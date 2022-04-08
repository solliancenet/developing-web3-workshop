# Solana

Duration: ~2 hours

This lab will take you thru a client-side approach to working with the Solana blockchain.

In this lab you will:

- 🔌 Connect to a Solana cluster using the web3.js library

- 🏦 Generate a new keypair, then fund the resulting address with an airdrop

- 💸 Transfer tokens between accounts

- ⛓ Deploy and interact with a Solana program (aka Smart Contract), written in Rust

1. With your Gitpod ready to use, within the **Simple Browser** tab, scroll down until you see the Chains listing.

2. Select **Solana**.

    ![Graphical user interface, application Description automatically generated](./images/media/image9.png)

## Welcome to the Solana Pathway

1. Read the overview instructions that appear for the Pathway. This first step does not require you to make any code changes, it's just an overview of the approach so you know what to expect.

2. When you've finished reading the overview, look for a large navigation button labeled **Setup the Project** near the bottom right of the **Simple Browser** panel and select that.

    ![](./images/media/image42.png)

## Setup the project

1. The first thing you need to do in this step is to install the Solana CLI. To install the CLI into your GitPod instance, follow these steps:

   1. Near the bottom right of the **Simple Browser** panel, at the top of the terminal panel, select the **+** button and then select **bash** to create a new bash shell instance.

        ![Graphical user interface, application Description automatically generated](./images/media/image43.png)

   2. Within the bash shell that appears, paste the following command to download and install the Solana CLI.

        ```bash
        sh -c "$(curl -sSfL https://release.solana.com/v1.10.6/install)"
        ```

        ![Text Description automatically generated with low confidence](./images/media/image44.png)

   3. When it finishes you will see a note to close and reopen your terminal to apply the path changes however, you can also simply run the following command to add the Solana CLI path to your active terminal session:

    ```bash
    export PATH="/home/gitpod/.local/share/solana/install/active_release/bin:$PATH"
    ```

2. Confirm you have Solana installed by running:

    ```bash
    solana --version
    ```

3. You should see output similar to the following:

    ![](./images/media/image47.png)

4. Next you will need to get you DataHub API keys. In this step, right click the **Signup for DataHub account** [link](https://datahub.figment.io/signup) and select to open that in new tab in your browser.

    ![Graphical user interface, text, application, chat or text message Description automatically generated](./images/media/image11.png)

5. Switch to that tab and complete the registration for the free DataHub account.

    ![Graphical user interface, text, application, email Description automatically generated](./images/media/image12.png)

6. Confirm your e-mail address.

    ![Graphical user interface, text, application, email Description automatically generated](./images/media/image13.png)

    ![Graphical user interface, application, PowerPoint Description automatically generated](./images/media/image14.png)

7. Login to Datahub with the credentials you created

    ![Graphical user interface, text, website Description automatically generated](./images/media/image15.png)

8. Return to the Gitpod environment and follow the instructions for acquiring a DataHub key and adding to your code.

9. Be sure to select Solana as the protocol when creating your app in DataHub!

10. When you have copied the key, you will need to create a `.env.local` file in which to store it. Follow these steps:

    1. From the left treeview of the Gitpod environment under the root folder `/learn-web3-dapp` locate the file `.env.example`.

    2. Right click the file and select Rename. Change the name to `.env.local`

    3. Double click the `.env` file to open it in a new editor panel.

    ![Graphical user interface, application Description automatically generated](./images/media/image16.png)

11. Paste your key as instructed and close the `.env.local` tab.

    > NOTE: Whenever the instructions tell you edit code, look for the code file in the Explorer tree view just as you did for the `.env.local` file.

12. Select the navigation button **Connect to Solana** to continue.

## Connect to Solana

1. Follow the instructions to edit the `connect.ts` file.

2. Make sure to select **Network-\>Devnet** before selecting connect otherwise you will see an error.

3. When complete you should see something like:

    ![](./images/media/image48.png)

4. Select the navigation button **Create an account** to continue.

## Create an account

1. Follow the instructions to edit the `keypair.ts` file. When complete you should see something like:

    ![](./images/media/image49.png)

2. Select the navigation button **Fund the account with SOL** to continue.

## Fund the account with SOL

1. Follow the instructions to edit the `fund.ts` file. When you select Fund this address you should see something like:

    ![Graphical user interface, text, application, chat or text message Description automatically generated](./images/media/image50.png)

2. Open the **View on Solana Explorer** link in a new browser tab and take moment to read the details of the transaction as it was captured in the blockchain. Look at the fee that was charged. Also, examine the Transfer Amount (SOL) to see how much was moved.

    ![A screenshot of a computer Description automatically generated](./images/media/image51.png)

3. Select the navigation button **Get the balance** to continue.

## Get the balance

1. Follow the instructions to edit the `balance.ts` file. When you select **Check Balance** you should see something like:

    ![Graphical user interface, text, application, chat or text message Description automatically generated](./images/media/image52.png)

2. Select the navigation button **Transfer some SOL** to continue.

## Transfer some SOL

1. Follow the instructions to complete the code in the `transfer.ts` file.

2. Provide the amount to transfer and select **Generate an address** to create a random address to transfer the test funds to.

    ![Graphical user interface, text, application Description automatically generated](./images/media/image53.png)

3. Then select **Submit Transfer**, you should see something like:

    ![Graphical user interface, text, application, chat or text message Description automatically generated](./images/media/image54.png)

4. Take a look at the transaction on the Solana explorer by selecting the **View on Sollance Explorer* link and opening in a new window.

5. Select the navigation button **Deploy a program** to continue.

## Deploy a program

1. Follow the instructions and execute the commands provided in your Gitpod terminal, this includes:

    - Run the following to install Rust:

        ```bash
        curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
        ```

    - Setup Solance

        ```bash
        solana config set --url https://api.devnet.solana.com
        ```

    - Create a keypair

        ```bash
        mkdir solana-wallet
        solana-keygen new --outfile solana-wallet/keypair.json
        ```

    - Perform an airdrop

        ```bash
        solana airdrop 1 $(solana-keygen pubkey solana-wallet/keypair.json)
        ```

    - Check the balance

        ```bash
        solana config get
        solana account $(solana-keygen pubkey solana-wallet/keypair.json)
        ```

    - Compile the program

        ```bash
        yarn run solana:build:program
        ```

    - Deploy the program

        ```bash
        solana deploy -v --keypair solana-wallet/keypair.json dist/solana/program/helloworld.so
        ```

    - Change the Solana target cluster, and start the validator:

        ```bash
        solana config set --url http://127.0.0.1:8899

        solana-test-validator
        ```

    - Open a new terminal window, select **+->bash**

    - Run the following to create an airdrop:

        ```bash
        export PATH="/home/gitpod/.local/share/solana/install/active_release/bin:$PATH"

        solana airdrop 100 $(solana-keygen pubkey solana-wallet/keypair.json)
        ```

2. When you get to the pathway **Challenge**, as per the instructions, be sure you go back to the **Connect to Solana** step and change the Network to `localnet`.

3. You don't have the complete the code, but you do need to complete each step again (such as funding the account).

4. Once you have switched to the `testnet`, the output of your deployment includes the program ID you will need to paste into the text box before selecting **Check Deployment**.

    ![Text Description automatically generated](./images/media/image55.png)

5. Copy that value and paste it into the text box similar to the following:

    ![Graphical user interface, text, application, chat or text message, email Description automatically generated](./images/media/image56.png)

6. Then proceed with completing the code for the `deploy.ts` file. When you have done so and selected **Check Deployment**, you should see something similar to the following:

    ![Graphical user interface, text, application, chat or text message Description automatically generated](./images/media/image57.png)

7. Select the navigation button **Create storage for the program** to continue.

## Create storage for the program

1. Follow the instructions to edit the `greeter.ts` file, you should see something similar to the following when successful:

    ![Graphical user interface, text, application, chat or text message Description automatically generated](./images/media/image58.png)

2. Select the navigation button **Get data from the program** to continue.

## Get data

1. Follow the instructions to edit the `getter.ts` file, you should see something like the following when successful:

    ![](./images/media/image59.png)

2. Select the navigation button **Send data to the program** to continue.

## Send data

1. Follow the instructions to edit the `setter.ts` file

2. Select the navigation button **Pathway Complete** to continue.
