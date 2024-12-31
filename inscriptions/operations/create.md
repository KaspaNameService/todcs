# Create

## Text inscriptions

Inscribe general texts and content on Kaspa.

### Typescript example

```ts
const data = "abc";
const buf = Buffer.from(data);
const script = new ScriptBuilder()
  .addData(XOnlyPublicKey.fromAddress(account).toString())
  .addOp(Opcodes.OpCheckSig)
  .addOp(Opcodes.OpFalse)
  .addOp(Opcodes.OpIf)
  .addData(Buffer.from("kns"))
  .addI64(0n)
  .addData(buf)
  .addOp(Opcodes.OpEndIf);
```

## Domain inscriptions

Create domains on Kaspa.

- Domains are registered in a first-come, first-serve basis
- Fees have to be paid to the KNS receiving address in output 1 of the reveal transaction
  - Testnet 10 payment address: `kaspatest:qq9h47etjv6x8jgcla0ecnp8mgrkfxm70ch3k60es5a50ypsf4h6sak3g0lru`
- Domains follow the same standard as [ENS](https://docs.ens.domains/faq#what-characters-are-supported)
- JSON format
  | key | required | description |
  | --- | -------- | --------------------------------------------------------------- |
  | op | yes | operation. "create" |
  | v | yes | inscription value. length has to be greater than 1. |
  | p | yes | protocol. "domain" |
  | s | no | the domain suffix, defaults to .kas, currently only .kas |

### Fees

- Testnet (price in kaspa). char indicates character length of the string
  | | 1 char | 2 char | 3 char | 4 char | 5 char |
  |-------|--------|--------|--------|--------|--------|
  | Price | 6 | 5 | 4 | 3 | 2 |

### Typescript example

This would create a `example.das` domain

```ts
const data = JSON.stringify(
  { op: "create", p: "domain", v: "example" },
  null,
  0
);
const buf = Buffer.from(data);
const script = new ScriptBuilder()
  .addData(XOnlyPublicKey.fromAddress(account).toString())
  .addOp(Opcodes.OpCheckSig)
  .addOp(Opcodes.OpFalse)
  .addOp(Opcodes.OpIf)
  .addData(Buffer.from("kns"))
  .addI64(0n)
  .addData(buf)
  .addOp(Opcodes.OpEndIf);
```

## Inscriptions of other mimeTypes

- hex string of the file data

### Typescript example

```ts
const mimeType = "image/jpeg";
const data = (file as Buffer).toString("hex");
const script = new ScriptBuilder()
  .addData(XOnlyPublicKey.fromAddress(account).toString())
  .addOp(Opcodes.OpCheckSig)
  .addOp(Opcodes.OpFalse)
  .addOp(Opcodes.OpIf)
  .addData(Buffer.from("kns"))
  .addOp(1)
  .addOp(1)
  .addData(Buffer.from(mimeType))
  .addI64(0n)
  .addData(data)
  .addOp(Opcodes.OpEndIf);
```
