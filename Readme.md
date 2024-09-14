## PROBLEM STATEMENT

In cloud computing environments, efficiently scheduling Virtual Machines (VMs) onto a limited number of servers is a critical and complex task. Given M VMs and N servers (where M >> N),\
VM-1=>N\
VM-2=>N\
VM-3=>N\
..\
..\
VM-M=>N

the problem becomes exponentially complex, with a total of M^N possible configurations. This combinatorial nature renders VM scheduling an NP-hard problem, making it challenging to achieve optimal resource utilization.

Traditional VM scheduling algorithms rely on static or heuristic-based approaches, which often result in suboptimal server states—either underloaded, overloaded, or balanced—depending on the varying demands placed on the infrastructure. These methods typically involve three key stages: VM selection, VM placement, and VM migration. However, they may not effectively anticipate the dynamic nature of incoming workloads, leading to inefficiencies such as increased energy consumption, longer processing times, and reduced overall system performance.

The objective of this project is to address these challenges by leveraging AI/ML techniques to predict CPU workloads in advance, enabling a more informed and proactive VM scheduling strategy. By accurately forecasting the expected workload, the system can preemptively allocate resources, thereby optimizing VM placement and reducing the need for reactive scheduling interventions. The AI/ML-based approach aims to converge on an optimal balance between energy consumption and processing time, ensuring that the cloud infrastructure operates at peak efficiency.

This predictive model will be benchmarked against traditional heuristic approaches, which use pre-existing information to guide VM scheduling decisions. The comparison will focus on the effectiveness of workload predictions in minimizing scheduling overhead and achieving a more balanced server state, as well as the system’s ability to adapt to fluctuations in demand. The ultimate goal is to demonstrate that AI/ML-driven scheduling can not only enhance resource utilization but also significantly improve the overall performance and sustainability of cloud computing environments.


## Phase 1: Dataset and Modeling

In this phase, the project focused on collecting and preprocessing the CPU usage data, followed by the development of predictive models to forecast future CPU workloads. The steps undertaken in this phase are outlined below:

1. Data Collection:
- CPU usage data was collected from CloudSim simulations, representing real-world cloud environments.
- The dataset originally consist of 348 files, each containing 288 CPU usage values. These files were merged into a single dataset with over 100,000 data points to facilitate comprehensive modeling.

2. Data Preprocessing:
- The raw data was cleaned and consolidated into a single dataset for easier analysis.
- Unnecessary columns were removed, and missing values were handled to ensure data quality.
- Feature engineering was performed by creating a "Next_CPU_Usage" column, shifting the data to model future predictions.

3. Modeling:
Three predictive models were applied to forecast the CPU usage:
- Decision Tree Regressor
- Random Forest Regressor
- Gradient Boosting Regressor
These models were trained on the preprocessed dataset and evaluated using metrics such as Mean Squared Error (MSE) and R-Squared (R2) score to gauge prediction accuracy.

4. Results:
- The models were compared based on their ability to predict the next 5 CPU usage values. The evaluation metrics indicated that the Random Forest model provided the best performance, but further optimization is required to improve accuracy.

