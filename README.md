# Akash Reinvest Script (LINUX BASH) #

----------
## Overview ##
This is a linux bash shell script that is designed to work with the **Akash Network** and a local Akash Wallet. 

Using CRON this script can be used to enable the automated withdrawal of Staked Rewards and Reinvestment of these Rewards with an operating Validator on the Akash Network.

## Usage ##
*Ensure all of the **configuration steps** have been completed before attempting to run the batch script.*

To run the script just open a Command Window and run the batch File. 

    # ./akash_reinvest

Your output should look similar to the following;

![](https://i.imgur.com/0QnXSYv.png)

If you do not have a sufficient balance for the re-staking to occur this will be the results the script will produce;

![](https://i.imgur.com/lDi6mGu.png)

A few quick notes;

1. The script always generates re-staking amount in whole integers
2. The script can take up to 45 seconds to execute due to timeout delays
3. You can run the script as frequently as you want, just be aware that you get charged 2 sets of fees each time the script executes - One fee to **Withdraw** your rewards, and another fee to **Delegate/Restake** your rewards.

## Configuration Steps ##
To configure your machine for executing this batch script you need to complete each of the steps below;

### Install JQ ###
**What is jq** - jq is like `sed` for JSON data - you can use it to slice and filter and map and transform structured data with the same ease that sed, awk, grep and friends let you play with text.

**Step 1** - Visit the jq download page - [https://stedolan.github.io/jq/download/](https://stedolan.github.io/jq/download/) for details on how too install jq to your linux machine via your package manager.



### Akash Installation ###
This will install the Akash binaries onto your local Linux machine;

**Step 2** - Visit the Akash GitHub site ( [https://github.com/ovrclk/akash/releases/latest](https://github.com/ovrclk/akash/releases/latest) ) and download the latest version of the Akash software for Linux. At the present time the latest version is v0.12.1. Install Akash as per the directions contained in the README using GoDownloader which will place the compiled program into the `~/bin/` . 

All of our examples will refer to this "*Installation Folder*" as this location - `~/bin/`

**Step 3** - Test your installation - Using the below commands. This should produce results showing the current version of **Akash** that you have installed.

    # cd ~/bin
    # ./akash version
 

![](https://i.imgur.com/oVR4Rlr.png)

If your results are similar then you have successfully installed Akash.

### Akash Wallet Configuration ###

Now that you have Akash installed and operational. The following steps will walk you through the process of importing your existing wallet that was used for Staking Akash with a Validator. 

You can use wallets created using Keplr or wallets created using Cosmostation Mobile App. However, only wallets created with a 24 word mnemonic are compatible. 

**Step 4** - Import your wallet using your 24 word mnemonic. The command to use is, shown below (replace **[wallet_name]** with a name you want for your wallet);

    # ./akash keys add [wallet_name] --recover --keyring-dir .keys --keyring-backend test

You will be prompted for your 24 word mnemonic. Once entered, your wallet will be added to the local machine's keystore and your wallet address information will be displayed as shown below;

![](https://i.imgur.com/e44yVBn.png)

*Your results will not match the results shown* - The **name** you chose for your wallet will be displayed along with your wallet's specific **address** and **pubkey**.

### Script File (akash_reinvest) Configuration ###

The script file needs to be downloaded and configured before you can execute it with your installation. Follow these steps to complete the setup;

**Step 5** - download the **akash_reinvest** script file from github here - [https://github.com/ourlink/akash_reinvest_linux/blob/master/akash_reinvest](https://github.com/ourlink/akash_reinvest_linux/blob/master/akash_reinvest) and save the downloaded file to the same location on you machine as **akash**  (`~/bin`).

**Step 6** - Set the script to be executable by issuing the following command;

    # cd ~/bin
    # chmod +x akash_reinvest


**Step 7** - Using your favorite text editor (nano, vi, etc...) edit the `akash_reinvest` script file

![](https://i.imgur.com/zX6Quax.png)

In this step we are going to update the following options so that they contain your desired settings;

**AKASH_VALIDATOR** - this is the address of your validator for staking purposes. The address starts with `akashvaloper...`

- akash_validator=[paste in the validator address you want to re-stake your Akash to]

**KEY_ADDRESS** - this is the ADDRESS for your wallet. This is the address that was displayed to you in Step 4 above after importing your wallet.

- key_address=[paste in your wallet address]

**KEY_NAME** - This is the NAME that you called your wallet during the import in Step 4 above.

- key_name=[name of your key without quotes]

**RESERVE_AMT** - This is the amount of Akash (AKT) to leave in your wallet and not use for reinvesting. The amount is listed in atomic units (in our example, we have 5 AKT kept in reserve). We recommend to not set this amount too low! You must keep some Akash for payment of transaction fees.

- reserve_amt=5000000   (atomic representation of AKT)

**THRESHOLD_AMT** - This is the lowest amount of Akash (AKT) that will ever be Re-Staked. In other words, you can adjust this amount to save on transaction fees and set a minimum amount of Akash for re-staking. The amount is listed in atomic units (in our example, we have 2 AKT as the minimum).

- threshold_amt=2000000 (atomic representation of AKT)

## --DISCLAIMER -- ##
***WARNING** - This is a batch script which requires access to your Akash Wallet. Your Akash Wallet will reside on the local machine using the *`--keyring-backend test`* *setting. This setting opens up your wallet to anyone with access to your local machine. By using this batch script you acknowledge that you take full responsibility for the security of your Akash Wallet and this scripts execution.** 

## License ##
Released under the GNU General Public License v3

[http://www.gnu.org/licenses/gpl-3.0.html](http://www.gnu.org/licenses/gpl-3.0.html)
