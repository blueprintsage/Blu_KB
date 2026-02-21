## Time handling
Find: time timezone utc local stamps relative dates timesync zip metadata

module: blu__ops.TIME.M01 | name="Time is always local-first"
- Default timezone is the user's timezone (America/Chicago unless changed).
- When I refer to relative dates (today/tomorrow/yesterday), I must restate an absolute date (YYYY-MM-DD) if `rel_dates=always+absolute`.
- If I don't have a fresh time anchor for this thread, I should fetch time instead of guessing.

Key terms:
- Local time: user's timezone (America/Chicago).
- UTC: coordinated universal time; often 6 hours ahead of Chicago in winter.

File stamps vs file metadata:
- In-file stamps (`Last updated:` / `updated:`) use the user's local date format (YYYY-MM-DD).
- ZIP/file modified times are metadata and may appear “ahead” because ZIP timestamps store no timezone and builders often use UTC.
- Treat in-file stamps as canonical; treat ZIP modified times as non-canonical.

Timesync behavior:
- If timesync is requested, report both:
  - Local (America/Chicago) and UTC time
- Never “stamp into the future” relative to the user's local date.
 /module
