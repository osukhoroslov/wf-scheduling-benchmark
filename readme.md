# Benchmark for DAG Scheduling in Distributed Systems

This repository contains simulation-based benchmark for evaluating DAG scheduling algorithms designed for heterogeneous distributed computing systems. It is based on a large set of real-world DAG instances (currently scientific workflows) and realistic system configurations (currently clusters with multicore machines).

## Structure

- `dags` - contains files with DAG instances
- `systems` - contains files with system configurations
- `benchmark.yaml` - benchmark configuration file

## Installing simulator

For simulation purposes we use [DSLab DAG](https://github.com/osukhoroslov/dslab/tree/main/crates/dslab-dag), a library for studying the DAG scheduling algorithms. Clone the main branch of DSLab repository:

```
$ git clone https://github.com/osukhoroslov/dslab.git
```

To run DSLab DAG you will also need to [install Rust](https://www.rust-lang.org/tools/install). 

## Running experiments

Experiments are run with `dag-run-experiment` tool by passing it the path to benchmark configuration file:

```
$ cd dslab/tools/dag-run-experiment
$ cargo run --release -- --config PATH_TO_BENCHMARK_CONFIG
```

You can set the number of used threads with `--treads` option. By default, it uses all available CPU cores. 

After the benchmark execution is completed, its results are saved to file named `benchmark-results.json` in the same directory as benchmark config file. You can specify other path to save results with `--output` option.

## Results format

The results of benchmark are saved in JSON file. The file contains JSON array which elements correspond to individual simulation runs. Each run contains the following fields:

- `dag` - DAG instance
- `system` - system configuration
- `scheduler` - scheduling algorithm
- `completed` - whether the workflow execution completed successfully
- `makespan` - achieved makespan (workflow execution time)
- `exec_time` - simulation execution time (including algorithm execution time)
- `run_stats` - various collected metrics (see [documentation](https://osukhoroslov.github.io/dslab/docs/dslab_dag/run_stats/struct.RunStats.html))
