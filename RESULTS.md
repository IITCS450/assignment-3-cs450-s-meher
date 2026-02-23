# RESULTS: Lottery Scheduling + settickets

## Setup
- Processes: 2 child processes (A and B) + parent
- Tickets: A = 30, B = 10
- CPUs: ran xv6 with **CPUS=1** to force contention (with 2 CPUs and 2 busy processes, each child can run on its own CPU and tickets won’t noticeably affect share)
- Workload: each child runs a CPU-bound loop for a fixed time budget (ticks) and reports a work counter.

## Workload
Each child runs a CPU-bound loop for a fixed duration measured in ticks using `uptime()`.
Inside the loop it increments a counter (work units) as fast as possible, then prints the final count.
Higher counts indicate more CPU time received during the run.

## Observations
Trial 1:
- A (30): 1638002
- B (10): 513424
- Ratio A/B: 3.190

Trial 2:
- A (30): 1637728
- B (10): 513355
- Ratio A/B: 3.190

Trial 3:
- A (30): 1628004
- B (10): 511448
- Ratio A/B: 3.183

## Notes
Lottery scheduling is probabilistic, so results vary slightly run-to-run. Over longer runs the observed CPU share converges toward the ticket proportion (30:10 ≈ 3:1).
