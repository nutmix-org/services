# Hardware wallet project advancement

This document aims at describing the features related to skycoin hardware wallet and follow up their advancement.

## Firmware's features

This is the firmware for the skycoin device which is intended to safely store a "seed" corresponding to a skycoin wallet.

It can generate addresses, sign messages or transactions and check signatures.

The hardware wallet has two buttons: Ok and Cancel. The user has to press one of these buttons when the hardware wallet requires user confirmation.

It communicates with a host PC using a USB wire. Please use [Skycoin's web application](https://github.com/skycoin/skycoin) or [Skycoin Command line interface](https://github.com/skycoin/skycoin/tree/develop/cmd/cli) tools to communicate with this firmware.

More informations in tiny-firmware's [README.md](https://github.com/skycoin/services/blob/master/hardware-wallet/tiny-firmware/README.md) section 6. How to read the firmware's code.

### Firmware's security

#### 1. No message to get private key

The skycoin wallet is able to use a private key to sign any message and output the signature to the PC. But there is no way to have the firmware output the private key used to sign the message.

#### 2. After backup: no message to get the seed

The seed used to generate key pairs is stored in the firmware's memory.

This seed is important it represents the wallet itself.

For safety it is strongly recommended that the user keeps a backup of that seed handwritten in a paper stored somewhere safe.

This seed can be very useful to recover the wallet's money in case the skycoin hardware wallet is lost.

#### 3. Backup the seed

When the hardware wallet is freshly configured with a seed. The screen displays a **NEEDS BACKUP** message. This means that you can send a backup message to the hardware wallet to enter backup mode.

If a pin code was set (see [PIN code configuration section](# 5. PIN code protection)), it is required to enter backup mode.

The backup mode will display every word of the seed one by one and wait for the user to press the Ok button between each word. The user is supposed to copy these words on a paper (the order matters).

After a first round the words are displayed a second time one by one as well. The user is supposed to check that he did not mispelled any of these words.

Warning 1: once the backup is finished the **NEEDS BACKUP** disappears from the hardware wallet's screen and there is no way to do the backup again. If you feel you did not backup your seed properly better generate a new one and discard this one before you invested Skycoins on the wallet corresponding to that seed.

Warning 2: It is strongly recommended to do the backup short after the wallet creation, and before you invested Skycoins in it. If you loose a wallet that has an open door to do a backup, the person who finds it can use this backup to get the seed out of it. Especially if you did not [configure a PIN code](# 5. PIN code protection).

#### 4. Don't erase your seed

At the time this document is written the hardware wallet is only able to store one seed. **TODO ? new feature store more than one seed ?**

If the user sends a seed setting message, the hardware wallet's screen asks the user if he wants to write the seed. If the user presses hardware wallet's Ok button. The new seed is stored and if there was an other seed before, it is **gone forever**.

So don't configure a new seed on a hardware wallet that is representing a wallet you are still using (see [backup section](# 3. Backup the seed) to avoid this problem).

#### 5. PIN code protection

You can configure a PIN code on the hardware wallet. Check [this documentation](https://doc.satoshilabs.com/trezor-user/enteringyourpin.html) to see how to use the PIN code feature.

You can modify an existing PIN code. But the previous PIN code will be asked.

If you are not able to input a correct PIN code there is no way to change it apart from (wiping the device)[#### 6. Wipe the device].

#### 6. Wipe the device

A message exist to wipe the device. It erases seed and PIN code.

When the device receives a wipe message it prompts the user to confirm by pressing Ok button.

There is no way back after a wipe. All the stored data is lost.

#### 7. Passpharse protection

**TODO ?** [check this issue](https://github.com/skycoin/services/issues/134)
1) When to ask passphrase ?
2) Has impacts on web wallet integration

#### 8. Memory encryption

**TODO ?**
**Use passphrase as a key for encryption ?**

### Factory test mode

**TODO** [check this issue](https://github.com/skycoin/services/issues/133)

## Integration with the skycoin web wallet

[Skycoin's web application](https://github.com/skycoin/skycoin)

### Backup

**TODO** [check this issue](https://github.com/skycoin/skycoin/issues/1708)

### Pin code

**TODO** [check this issue for PIN code integration](https://github.com/skycoin/skycoin/issues/1765)

**TODO** [check this issue for PIN code configuration from the web wallet](https://github.com/skycoin/skycoin/issues/1768)

The PIN code can be configured from skycoin-cli using command:

    skycoin-cli deviceSetPinCode

**TODO** update cli's README.md about deviceSetPinCode command.

### Use many connected devices at the same time

**TODO** [check this issue](https://github.com/skycoin/skycoin/issues/1709)

### Wipe a device from the web wallet

**TODO** [check this issue](https://github.com/skycoin/skycoin/issues/1769)