#Chest Cancer Classification Using MLflow and DVC

This document provides an in-depth overview of a machine learning pipeline designed for the classification of chest cancer using **MLflow** and **DVC** (Data Version Control). The integration of these tools ensures a seamless workflow for reproducibility and model management in machine learning projects.

## Project Overview
This project encompasses the following key objectives:
- **Cancer Detection**: Utilize machine learning techniques to classify chest cancer from medical imaging data effectively.
- **Pipeline Management**: Leverage DVC for version control and management of datasets and models.
- **Experiment Tracking**: Employ MLflow to log experiments, track metrics, and manage model versions.

## Workflow Steps

### 1. Configuration File Updates

To initiate the pipeline, it’s essential to configure several files appropriately:

- **`config.yaml`**: Adjust settings such as input data paths, model specifications, and output directories. This file serves as a central configuration hub for various pipeline components.
- **`secrets.yaml`** (Optional): For sensitive information such as API keys or passwords, use this file. This allows for better security management.
- **`params.yaml`**: Modify hyperparameters related to model training and evaluation, such as the learning rate, batch size, and number of epochs.

### 2. Define the Entity
The entity typically refers to the project context in which the data is being processed. Ensure that you define the entity correctly as it can affect data lineage tracking in MLflow.

### 3. Update the Configuration Manager
In the `src/config` directory, update the configuration manager to dynamically load configurations from the YAML files. This component allows the rest of the code to access these configurations seamlessly.

### 4. Update the Components
You may need to refine individual components of your pipeline, such as data loading, preprocessing, feature extraction, and model definition. Each component should be modular to facilitate reusability and testing.

### 5. Revise the Pipeline
Ensure that the entire pipeline – data preparation, training, evaluation, and inference – is properly defined. This allows for easier debugging and validation. Utilize DVC commands to streamline this process.

### 6. Edit `main.py`
Make necessary adjustments to the main execution script that controls the flow of the application, including argument parsing for command-line interactions.

### 7. Update the `dvc.yaml`
DVC uses this file to track the stages in your pipeline. Sync any changes made to the components of the pipeline with this configuration, ensuring all steps are covered and properly sequenced.

## MLflow Integration

### Key Features
**MLflow** provides the following functionalities:
- **Experiment Tracking**: Log various metrics during training, enabling you to compare different runs effortlessly.
- **Model Registry**: Store, annotate, and access versions of models.
- **Deployment**: Simplify the process of deploying models to various environments.

### Useful Resources
- **MLflow Documentation**: [Official Documentation](https://mlflow.org/docs/latest/index.html)
- **MLflow Tutorial Series**: [YouTube MLflow Playlist](https://youtube.com/playlist?list=PLkz_y24mlSJZrqiZ4_cLUiP0CBN5wFmTb&si=zEp_C8zLHt1DzWKK)

### Command to Launch MLflow UI
To visualize your experiments, use the following command:
```bash
mlflow ui
```
Navigate to `http://localhost:5000` in your browser to access the MLflow UI.

### DagsHub Integration
To track MLflow experiments in DagsHub:
```bash
export MLFLOW_TRACKING_URI=https://dagshub.com/entbappy/chest-Disease-Classification-MLflow-DVC.mlflow
export MLFLOW_TRACKING_USERNAME=entbappy 
export MLFLOW_TRACKING_PASSWORD=6824692c47a4545eac5b10041d5c8edbcef0
python script.py
```
This setup allows you to monitor and manage experiments remotely.

### DVC Command Overview
Key DVC commands to manage your workflow:
1. **Initialize DVC**:
   ```bash
   dvc init
   ```
   This sets up a new DVC repository.
   
2. **Reproduce the DVC Pipeline**:
   ```bash
   dvc repro
   ```
   This command executes all the stages of your defined pipeline.

3. **Visualize the Pipeline**:
   ```bash
   dvc dag
   ```
   Generate a graphical representation of the pipeline stages and dependencies.

## Understanding MLflow and DVC

### MLflow
MLflow is designed for:
- **Production-Grade**: It supports the entire ML lifecycle.
- **Experiment Tracking**: Easy logging and tagging of models.
- **Flexible Deployment**: Facilitates smooth transitions from development to production.

### DVC
DVC serves as:
- **Lightweight**: Ideal for rapid prototyping and proof of concept projects.
- **Version Control**: Manage experiments and datasets efficiently.
- **Pipeline Orchestration**: Create complex pipelines with minimal overhead.

## AWS CI/CD Deployment Using GitHub Actions

### Steps for AWS Setup

1. **Login to AWS**: Access the AWS Management Console.
2. **Create an IAM User**:
   - Assign necessary permissions.
   - **EC2 Access** for managing your virtual machines.
   - **ECR Access** for storing Docker images.

3. **Establish an ECR Repository**: Save the repository URI (e.g., `566373416292.dkr.ecr.us-east-1.amazonaws.com/chicken`).
   
4. **Provision an EC2 Instance**: Deploy an Ubuntu instance to host your application.

5. **Install Docker on EC2**:
   - Run updates:
     ```bash
     sudo apt-get update -y
     sudo apt-get upgrade
     ```
   - Install Docker:
     ```bash
     curl -fsSL https://get.docker.com -o get-docker.sh
     sudo sh get-docker.sh
     sudo usermod -aG docker ubuntu
     newgrp docker
     ```

6. **Configure EC2 for GitHub Actions**:
   - Go to GitHub settings and set up a self-hosted runner under `Settings > Actions > Runners > New Self-Hosted Runner`. Follow the prompts to configure your runner.

7. **Set Up GitHub Secrets**:
   - Store sensitive information as secrets in your GitHub repository:
     - `AWS_ACCESS_KEY_ID=<your_key>`
     - `AWS_SECRET_ACCESS_KEY=<your_secret>`
     - `AWS_REGION=us-east-1`
     - `AWS_ECR_LOGIN_URI=<repository_uri>`
     - `ECR_REPOSITORY_NAME=<repo_name>`

### Deployment Process Summary
- Build Docker images from your source code.
- Push Docker images to ECR.
- Launch the EC2 instance.
- Pull Docker images from ECR to EC2.
- Start your application in a Docker container on EC2.

## Conclusion
By following this guide, you will set up a comprehensive machine learning pipeline for chest cancer classification that integrates effective version control and experiment tracking practices. This robust framework allows for continuous improvement and deployment of your machine learning models, ensuring that your results are reproducible and easily manageable.
