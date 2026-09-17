# seatsherpa-uptime

A GitHub Actions workflow that probes Seat Sherpa's database API every five minutes.

- `.github/workflows/health.yml` requests one public row (`app_config`) from the Supabase REST endpoint with a 15 second timeout, twice.
- If both attempts fail, the run fails, so GitHub sends its normal failed-run email, and on the first failure an edge function emails the founder. When the next run succeeds, one recovery email goes out.
- Nothing sensitive lives here. The API key and the alert bearer are repository secrets.

Why a public repo: scheduled workflows on public repositories run for free without a minutes quota; the probe would exceed a private repository's free minutes within days.

Manual run: Actions → Supabase health → Run workflow.
