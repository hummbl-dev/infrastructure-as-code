# Invalid Fixture Coverage

`environment-contract-v0.1.invalid.json` is intentionally a combined negative
fixture for the initial v0.1 packet. It exercises these schema gates:

- `infrastructureManifest.version` must be at least `1`.
- `authority.canActOnBehalfOf` must not be empty.
- `infrastructureContract.environment.piiPolicy` must match the allowed enum.
- `infrastructureContract.topology.components[].id` must match the component id pattern.
- `infrastructureContract.topology.networkZones` must not be empty.
- `infrastructureContract.dependencies.requiredServices` must not be empty.
- `infrastructureContract.dependencies.secretBoundary` must match the allowed enum.
- `infrastructureContract.changeControl` numeric limits must be at least `1`.
- `infrastructureContract.rollback.maxDowntimeMinutes` must be at least `1`.
- `infrastructureContract.validation.validationSamples` must be at least `1`.
- `infrastructureContract.validation.negativeCasesCovered` must not be empty.
- `receiptRequirements` fields must be non-empty receipt references.

Future packets may split these into one-fixture-per-rule cases once the schema
test harness supports named negative assertions.
