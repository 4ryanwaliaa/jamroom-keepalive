# Jam Room Render health check

A small GitHub Actions health check for the Jam Room Spotify authorization prototype. It uses no GPT, Codex automation, Firebase credentials, Spotify credentials, checkout action, dependency installation, or persistent access token. The application source remains in a separate private repository.

The workflow requests the configured Render `/health` endpoint once every 10 minutes. It accepts only HTTP 200 with JSON `status` equal to `ok`. Redirects are not followed, the response is bounded to 64 KiB, and the request has a 90-second timeout. Only a generic result is logged; response bodies are not printed.

## Activate after Render deployment

Add the repository Actions variable `RENDER_HEALTH_URL` with the actual assigned service URL followed by `/health`, for example `https://ACTUAL-SERVICE.onrender.com/health`. Use the real deployed Jam Room service. Until this variable is set, jobs skip before allocating a runner and no HTTP requests are sent.

Use **Actions > Jam Room Render keep-alive > Run workflow** to check it immediately. No computer or Codex app needs to stay open. The schedule exists on the default `main` branch.

## Free operation and limits

This repository is public and contains only the monitoring workflow and documentation. Standard GitHub-hosted runners for public repositories are free. Do not move this frequent schedule into a private repository without accounting for its shared Actions allowance.

GitHub may delay or drop scheduled runs. Public scheduled workflows are disabled after 60 days without repository activity. Render may still restart or suspend services under its own shared free-plan quotas. This check cannot guarantee continuous uptime and does not test Firebase authentication, Spotify consent, stored credentials, or music playback.

References: [GitHub scheduled workflows](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows#schedule), [GitHub Actions billing](https://docs.github.com/en/billing/concepts/product-billing/github-actions), [Render Free limits](https://render.com/docs/free).
