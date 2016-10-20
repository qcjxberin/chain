# Keys

## Introduction

Cryptographic private keys are the primary authorization mechanism on a blockchain. They control both the issuance and transfer of assets. Each transaction is signed using the specific private keys required for the issuance or transfer it proposes, and the signature is checked against the corresponding public keys recorded in the earlier transaction being spent, or the asset type being issued, in order to determine the new transaction’s validity.

In a production environment, private keys are generated within an HSM (hardware security module) and never leave it. Their corresponding public keys are exported for use within Chain Core. In order to issue or transfer asset units on a blockchain, a transaction is created in Chain Core and sent to the HSM for signing. The HSM signs the transaction without ever revealing the private key. Once signed, the transaction can be submitted to the blockchain successfully.

For development environments, Chain Core provides a convenient MockHSM. The MockHSM API is identical to the HSM API in [Chain Core Enterprise Edition](https://chain.com/enterprise), providing a seamless transition from development to production. It is important to note that the MockHSM does not provide the security of a real HSM.

## Overview

This guide will walk you through the basic key operations:

* Create key (in the MockHSM)
* Load key (into the HSM Signer)
* Sign a transaction (with the MockHSM)

### Sample Code
All of the code samples in this guide are extracted from a single, runnable Java file.
<a href="../examples/java/Keys.java" class="downloadBtn btn success" target="_blank">View Sample Code</a>

## Create key

Create a new key in the MockHSM. (Requires a context to have been created with `new Context()`.)

$code ../examples/java/Keys.java create-key

## Load key

To be able to sign transactions, load the key into the HSM Signer, which will communicate with the MockHSM.

$code ../examples/java/Keys.java signer-add-key

## Signing transactions

Once a transaction is built, send it to the HsmSigner for signing.

$code ../examples/java/Keys.java sign-transaction

[Download Code](../examples/java/Keys.java)