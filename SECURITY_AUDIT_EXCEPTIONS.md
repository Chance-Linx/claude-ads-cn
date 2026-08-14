# Security Audit Exceptions

Snapshot date: 2026-08-14

The CI dependency audit intentionally keeps `pip-audit --strict` enabled. The
current lock also carries explicit temporary ignores for the advisory IDs below.

## Current Exceptions

- `cryptography 48.0.1`
  - `PYSEC-2026-3552`
  - `PYSEC-2026-3553`
  - `PYSEC-2026-3554`
- `pillow 12.2.0`
  - `PYSEC-2026-2253`
  - `PYSEC-2026-2254`
  - `PYSEC-2026-2255`
  - `PYSEC-2026-2256`
  - `PYSEC-2026-2257`
  - `PYSEC-2026-3451`
  - `PYSEC-2026-3452`
  - `PYSEC-2026-3453`
  - `PYSEC-2026-3454`
  - `PYSEC-2026-3493`
  - `PYSEC-2026-3494`
  - `PYSEC-2026-3495`
  - `PYSEC-2026-3496`

## Reason

The reviewed dependency inventory is bound to a CPython 3.11/3.12 Linux,
macOS, and Windows wheel matrix. A direct upgrade currently changes the
available wheel set and Linux/macOS compatibility assumptions:

- `pillow 12.3.0` does not provide the same manylinux2014 x86_64 wheel target
  used by the current release evidence.
- `cryptography 50.0.0` changes macOS wheel availability relative to the
  current macOS Intel and Apple Silicon target evidence.

Because the release verifier treats dependency inventory, wheel hashes, and
platform coverage as reviewed evidence, this fork should not silently rewrite
those constraints just to clear the audit.

## Review Rule

Remove these exceptions only after the dependency inventory, native target
evidence, lock files, release verifier policy, and installer matrix have been
reviewed together.
