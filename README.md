# xl1-status-data

Machine-written status for the XL1 block producers behind
[winlew.co/xl1](https://winlew.co/xl1/). Two nodes push here every five minutes;
nothing else does.

    windows.json    the Windows producer
    rbpi3.json      the Raspberry Pi producer

## Why this repo exists separately

The status pages used to live in the same repository as their data, so every
five-minute data update triggered a full site deploy — about 550 deploys a day
to change one JSON file. That exhausted the host's monthly build allowance and
the pages froze, still serving an hour-old snapshot and honestly reporting
themselves stale while both producers were healthy.

Splitting the data out means the site deploys only when the site changes. The
pages read these files directly, so an update is visible as soon as the CDN
cache turns over.

## Why it is public when the site repository is not

These files are the same allow-listed projection already served on the public
status pages — the dashboard's `/api/public` endpoint, which is built from an
explicit list of fields rather than by removing sensitive ones, and is tested
against a payload seeded with canary values. Publishing them here exposes
nothing that winlew.co/xl1 does not already show to anyone who visits.

What stays private is the site and node configuration: addresses of internal
services, alert routing, host details, and everything else not on that list.

## Do not send pull requests

Every file here is overwritten by a machine on a five-minute timer. Changes
would be gone before anyone read them. If something looks wrong, the producers
are at [winlew.co/xl1](https://winlew.co/xl1/).

## Reading it

Both files carry a `generatedAt` timestamp and a `schema` version. Check the
timestamp before trusting the numbers — a node that has stopped publishing
leaves its last file in place, and stale data looks exactly like fresh data if
you do not look at the clock.
