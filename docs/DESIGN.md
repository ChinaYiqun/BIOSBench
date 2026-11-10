# Design notes (proposal)

## Unit of evaluation
A task is a pinned upstream revision, an agent-visible natural-language issue, an allowed source subtree, and an independent build/behavioral oracle. Every task must be manually verified as solvable before inclusion.

## Reproducibility checklist
- Pin upstream commits and toolchains; pin OCI image digests (not latest tags).
- Start from a clean worktree, capture the resulting patch, enforce time and memory budgets.
- Keep hidden tests outside the agent container; evaluate patch in a second fresh container.
- Distinguish infrastructure errors from task failures, but include task failures in resolved-rate denominator.
- Capture QEMU console/serial logs, exit status, structured assertions, and checksums.
- Check licenses and do not ship proprietary firmware, blobs or vendor secrets without authorization.

## Validity threats
QEMU does not emulate all platform-specific initialization. Compiling OVMF cannot validate SMM, silicon bring-up or physical board electrical behavior. Provide hardware-specific tracks only when independent hardware tests are available.

## Benchmark integrity
Do not conflate agent model and harness. Fix task budget, compare agent+model+tools as systems, and distinguish model-only experiments. Publish task provenance and leakage controls. Do not report numeric results until run protocol is frozen.
