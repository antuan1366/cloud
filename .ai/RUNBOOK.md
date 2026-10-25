# Runbook

Status: initial skeleton. Local checks below are read-only. No AWS provisioning command is approved by this document.

## Windows PowerShell — Git check
Run:
    git --version
Expected: a Git version string. If command is not recognized, Git is unavailable on PATH.

Check VMware Workstation in Start menu or installed apps. Do not assume it is installed.

## Linux VM — checks after the VM exists
    uname -a
    git --version
    terraform version
    ansible --version

These checks work only after the relevant tools are installed.

## Terraform local validation
From the directory containing Terraform configuration:
    terraform fmt -check
    terraform validate

terraform validate may require terraform init first. Init downloads provider/plugin packages but does not by itself create the described AWS infrastructure. Review files and commands before running them.

## AWS provisioning gate
Do not run terraform apply or manually create AWS resources until current account terms/credit eligibility, pricing, ongoing charges, and cleanup have been reviewed and the user has explicitly approved.

## Teardown gate
Never run terraform destroy blindly. Check workspace, state, and destroy plan; confirm it targets only this lab; confirm data loss is acceptable; obtain approval; then verify remaining billable resources in AWS Console.

## Recording verified operations
For each operational command, record OS/shell, working directory, prerequisites, exact command, expected output, actual result/date, and side effects/cost implications.
