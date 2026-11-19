# Assignment 2 — final review and submission

The deployment report is [deployment.md](deployment.md). The diagram is available as a (image-3.png).

## Verify the final application

Run from a terminal with internet access and retain the output:

```bash
curl -I http://54.175.182.10
```

Expect successful TLS validation and HTTP 200

## Optional resilience evidence

Before claiming tested failover, perform a controlled test during a suitable maintenance window:

1. Confirm both targets are Healthy and identify the SSH session for app-02.
2. On app-02 only, stop the backend: `sudo systemctl stop travelmemory-backend`.
3. Wait for that target to become Unhealthy and confirm app-01 remains Healthy.
4. Verify the custom-domain page and `/api/trip` remain available after health-check convergence. Requests may fail during detection; do not claim zero downtime without measurements.
5. Restore app-02: `sudo systemctl start travelmemory-backend`.
6. Wait for both targets to become Healthy again and record the result.

Do not stop both backends. The user has since performed a one-VM shutdown: intermittent 504s occurred initially, then service stabilized without changes after waiting. Eventual failover is user-confirmed; zero downtime is not demonstrated. Restore the stopped instance and confirm both targets become Healthy. Target-state screenshots and measured detection/recovery times would strengthen the evidence. See section 14 of the deployment report.

## Package the repository

The local Git checkout is `TravelMemory/`. Both `docs/` and `deploy/` are now inside it, so the report, images, diagram, Nginx configuration, and service definition can be committed with the application. Keep the relative `docs/` and `deploy/` layout together and stage both directories before committing.

The frontend and backend source files are unchanged from the original application. Suggested troubleshooting source edits were removed from the submission. Keep deployment-specific settings in environment files and the supplied infrastructure configuration; do not commit actual database credentials or overwrite the server `.env`.

Confirm rotation of the database password exposed during troubleshooting. Review staged files for `.env`, private keys, connection strings, and credentials before committing. The repository's existing `.env` ignore rule is useful but does not replace inspecting the staged file list.

Commit and push to the intended repository, then check the GitHub page renders the report's screenshots and architecture preview. Verify the latest commit and remote branch before submitting.

## Submit through Vlearn

Place the final repository URL in the text, Word, or PDF format permitted by the assignment and submit it through Vlearn. The currently configured origin is `git@github.com:i-adityaverma/TravelMemory.git`, corresponding to:

https://github.com/i-adityaverma/TravelMemory

Verify the pushed repository contains the final artifacts before using that link for submission.
