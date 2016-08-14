decrypt-kms-env
---------------
Simple util for decrypting secure environment variables encrypted using KMS. Follows a simple convention whereby:

- Encrypted blobs are prefixed with `secure:`,
- When the output of `decrypt-kms-env` is passed to `eval` in a shell, values are decrypted in-place

Before:

```sh
env

Secret1=secure:NNNNNNNN...
Secret2=secure:NNNNNNNN...
Secret3=secure:NNNNNNNN...
```

After:

```sh
eval $(decrypt-kms-env)
env

Secret1=cats
Secret2=dogs
Secret3=meow
```

### Install

Include `decrypt-kms-env` in your project's `package.json`. Once installed, run your application in your Dockerfile prefixed:

```
RUN eval $(./node_modules/.bin/decrypt-kms-env) && npm start
```

### Our usage

We use this from within Docker containers to decrypt env vars encrypted via KMS.
