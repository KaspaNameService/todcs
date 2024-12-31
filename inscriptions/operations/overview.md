# Inscription overview

Inspired by Ordinals & [Kasplex](https://docs.kasplex.org/), KNS inscriptions utilize scripts in transactions for applications such as KNS domains.

## Prerequisites

- The Kaspa wasm package, which can be gotten [here](https://github.com/kaspanet/rusty-kaspa/releases/). Example usage below:

```
import {
  Opcodes,
  ScriptBuilder,
  XOnlyPublicKey,
  type HexString,
} from "wasm/nodejs/kaspa/kaspa";
```
