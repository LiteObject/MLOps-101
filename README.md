# MLOps 101

Here is a Mermaid diagram illustrating the standard MLOps lifecycle activities, followed by an explanation of each stage.

### MLOps Lifecycle Diagram

```mermaid
flowchart TD
    A[Problem Definition & Business Understanding] --> B[Data Collection & Preparation]
    B --> C[Feature Engineering]
    C --> D[Model Development & Experimentation]
    D --> E[Model Validation & Evaluation]
    E --> F[Model Packaging]
    F --> G[Model Deployment]
    G --> H[Model Monitoring]
    H --> I{Performance Drift?}
    I -- Yes --> J[Model Maintenance & Retraining]
    J --> D
    I -- No --> H
    
    subgraph "Governance & Automation"
    K[CI/CD Pipelines] -.-> D
    K -.-> G
    L[Security & Compliance] -.-> B
    L -.-> G
    end
```

### Explanation of Activities

1.  **Problem Definition & Business Understanding**: This is the foundational stage where specific business objectives are identified (e.g., "predict stock price movements"). Success metrics are defined here to guide the rest of the project.

2.  **Data Collection & Preparation**: Raw data is gathered from various sources. This stage involves cleaning, formatting, and versioning the data to ensure it is usable for training. In your repository, this might involve scripts in `src` that fetch financial data.

3.  **Feature Engineering**: Raw data is transformed into meaningful features that machine learning algorithms can understand. This includes normalization, encoding, and selecting the most relevant variables.

4.  **Model Development & Experimentation**: Data scientists select architectures, train models, and tune hyperparameters. Experiment tracking is crucial here to log parameters and results.

5.  **Model Validation & Evaluation**: The model is tested against a holdout dataset to ensure it performs well on unseen data. Automated testing (like the contents of your `tests/` directory) ensures the code is robust before moving forward.

6.  **Model Packaging**: The model and its dependencies are bundled into a deployable format, often using containers.
    *   *Repo Context*: Your `Dockerfile` and `requirements.txt` are key components here, ensuring the environment is reproducible.

7.  **Model Deployment**: The packaged model is released into a production environment (e.g., a REST API or batch process).
    *   *Repo Context*: Your `docker-compose.yml` facilitates local or server deployment orchestration.

8.  **Model Monitoring**: Once live, the model is continuously monitored for performance degradation, errors, or latency issues.

9.  **Model Maintenance & Retraining**: If monitoring detects "drift" (where the model's accuracy drops because real-world data has changed), the model is retrained on new data, often triggering a loop back to the development stage.

10. **Governance & Automation**:
    *   **CI/CD**: Continuous Integration and Deployment pipelines (likely found in your `.github/` directory) automate testing and deployment tasks.
    *   **Security**: Ensuring data privacy and access controls throughout the lifecycle.
