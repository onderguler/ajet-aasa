# CMS configuration

Add the following path to the `DEEPLINKMANAGEMENT` entry whose ID is
`checkin`:

```text
/mobile-test/checkin
```

Optional environment mappings can use the same existing `checkin` ID:

```text
/mobile-dev/checkin
/mobile-preprod/checkin
/mobile-pilot/checkin
```

No application code change is required because the current deep-link manager
normalizes these paths and resolves CMS paths by exact or prefix match.
