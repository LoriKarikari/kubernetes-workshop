# Lab 1.04 - Automated Tasks - Jobs & CronJobs

## Introduction

Some workloads aren't meant to run continuously—they need to execute once and complete, or run on a schedule. Manual intervention for routine tasks isn't scalable.

In this exercise, you'll learn to automate operations by defining **Jobs** for one-time tasks and **CronJobs** for recurring scheduled tasks.

## Objectives

- Create a one-time **Job** to simulate a diagnostic task
- Deploy a recurring **CronJob** to run a task on a schedule
- Verify execution and logs to confirm successful automation

## Step-by-step: Deploying Jobs and CronJobs

### Step 01: Create a one-time Job

Use the declarative method to define a **Job** named `system-scan` that runs the `busybox` image and echoes:

```
Diagnostic scan complete.
```

### Step 02: Apply the Job and verify execution

Where can you find the output of the job?

### Step 03: Schedule a recurring task

Create a **CronJob** named `scheduled-task` that runs every 5 minutes using the `busybox` image to echo:

```
Scheduled task initiated.
```

Use the `*/5 * * * *` schedule format.

### Step 04: Apply and monitor the CronJob

### Step 05: Check logs from one of the CronJob runs

## Resources

- [Jobs](https://kubernetes.io/docs/concepts/workloads/controllers/job/)
- [CronJobs](https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/)
- [Automated Tasks with Cron Jobs](https://kubernetes.io/docs/tasks/job/automated-tasks-with-cron-jobs/)
