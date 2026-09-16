# oci-arm-retry

Asks Oracle Cloud every five minutes for the two Always Free Ampere A1
instances, because the capacity in `ap-hyderabad-1` is nearly always full — 1,241
attempts from a laptop over six days returned "no capacity" every single time.

There is no cleverer approach: you keep asking until capacity appears. The only
question is what does the asking, and a GitHub runner is better than a laptop
that has to stay awake for it.

This repository is public **only** so that Actions minutes are unlimited. It
contains the workflow and nothing else — no data, no keys. The Oracle
credentials live in GitHub's encrypted secret store, which is not readable from
forks or pull requests.

## Secrets it needs

| secret | what it is |
|---|---|
| `OCI_USER` | user OCID |
| `OCI_TENANCY` | tenancy OCID |
| `OCI_FINGERPRINT` | API key fingerprint |
| `OCI_REGION` | e.g. `ap-hyderabad-1` |
| `OCI_KEY` | the API private key, PEM |
| `OCI_PASSPHRASE` | passphrase for that key |
| `OCI_SUBNET` | subnet OCID to launch into |
| `OCI_IMAGE` | Ubuntu ARM image OCID |
| `OCI_SSH_PUB` | public key to put on the instance |

It stops on its own once two instances are running.

## Watch it

The Actions tab shows every attempt. A successful launch raises a notice on the
run, and the instance appears in the OCI console.

GitHub disables scheduled workflows after 60 days of repository inactivity, and
drops runs when its own load is high, so expect fewer attempts than the schedule
suggests. That costs nothing — capacity appears at random hours anyway.
