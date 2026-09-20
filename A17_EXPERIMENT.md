# pipa Android 17 Recovery Experiment

This branch is a device-tree preparation branch for HyperOS 4 / Android 17.
It is not a flashable recovery release.

The pipa-specific pieces intentionally remain unchanged:

- pipa kernel and DTB;
- pipa display geometry and touch configuration;
- pipa recovery fstab, including the FBE v2 inline-crypt and wrapped-key flags;
- pipa Keymaster 4.0/4.1 and Gatekeeper service declarations;
- `PRODUCT_SHIPPING_API_LEVEL := 30`, which represents pipa's launch API level.

Only recovery build identity is advanced to Android 17. A usable build must use
an Android-17-capable OrangeFox/TWRP recovery core. Rebuilding this tree against
the old `fox_12.1` core alone is expected to retain the current failure while
unwrapping `/metadata/vold/metadata_encryption/key/keymaster_key_blob`.

Observed failure with the current pipa A16 recovery:

```text
Keymaster status -62 (key blob requires upgrade)
Keymaster status -38 (upgrade operation fails)
```

Do not copy Keymaster, Gatekeeper, QSEE, RPMB, or other TEE-facing binaries
from another device. Those are device-bound and must remain pipa versions.
