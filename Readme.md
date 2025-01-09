# PROBLEM STATEMENT

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

# [Phase 1](https://github.com/suryansh4424/VM_Scheduler-CloudSim/tree/main/Phase%201): Data Analysis and Insight

To gather, prepare, and analyze the dataset to understand the CPU usage patterns. This will provide foundational insights for building predictive models and optimizing resource scheduling in subsequent phases.

## **1. Data Collection:**
- CPU usage data was collected from CloudSim simulations, representing real-world cloud environments.
- The dataset originally consist of 348 files, each containing 288 CPU usage values. These files were merged into a single dataset with over 100,000 data points to facilitate comprehensive modeling.

## **2. Data Preparation:**
### **Column Standardization:**
- Ensured consistency in column naming conventions, with Timestamp and CPU_Usage being cleaned and standardized for easier manipulation.

### **Timestamp Formatting:**
- Converted the Timestamp data into a proper datetime format (%d-%m-%Y %H:%M), ensuring correct interpretation of date and time values.

### **Feature Engineering:**
- Extracted the Hour from each timestamp to analyze CPU usage patterns on an hourly basis.

## **3. Data Analysis:**
### **Hourly CPU Usage Calculation:**
- The dataset was grouped by the hour of the day to compute the average CPU usage for each hour.
This analysis helped in visualizing CPU load distribution throughout the day and identifying periods of peak and low usage.

### **Peak Usage Identification:**
- By calculating the average CPU usage per hour, the peak hour (the hour with the highest average CPU load) was determined, providing insight into the time of day when system resources are most strained.

## **4. Results:**
The [CPU usage analysis](https://github.com/suryansh4424/VM_Scheduler-CloudSim/blob/main/Phase%201/CPU_usage_analysis.ipynb) revealed that the peak CPU usage occurred at Hour X, with an average CPU utilization of Y%.

# [Phase 2](https://github.com/suryansh4424/VM_Scheduler-CloudSim/tree/main/Phase%202): Model Development and Evaluation

To develop, evaluate, and refine machine learning models aimed at predicting CPU usage and optimizing scheduling strategies based on the insights gained from Phase 1 outlined below:

## **1. Data Preprocessing:**
- The raw data was cleaned and consolidated into a single dataset for easier analysis.
- Unnecessary columns were removed, and missing values were handled to ensure data quality.
- Feature engineering was performed by creating a "Next_CPU_Usage" column, shifting the data to model future predictions.

## **2. Modeling:**
Models were trained on the preprocessed dataset and evaluated using metrics such as Mean Squared Error (MSE) and R-Squared (R2) score to gauge prediction accuracy.
Three predictive models were comapred to forecast the CPU usage:
- Linear Regression
- Gated Recurrent Unit (GRU)
- Bidirectional LSTM
  
### 1. [**Linear Regression**](https://github.com/suryansh4424/VM_Scheduler-CloudSim/blob/main/Phase%202/Modeling/01_Linear%20Regression.ipynb)
- **R² Score**: ~0.62
- **Strengths**:
  - Simple and easy to implement.
  - Fast training and prediction time.
  - Comparable accuracy to more complex models.
- **Weaknesses**:
  - Assumes linear relationships, which may not fully capture complex patterns.

---

### 2. [**GRU (Gated Recurrent Unit)**](https://github.com/suryansh4424/VM_Scheduler-CloudSim/blob/main/Phase%202/Modeling/02_GRU%20Model.ipynb)
- **R² Score**: ~0.62
- **Strengths**:
  - Captures temporal dependencies in time series data.
  - Faster and less complex than LSTM.
- **Weaknesses**:
  - Longer training time compared to Linear Regression.
  - Minimal improvement in accuracy over simpler models.

---

### 3. [**Bidirectional LSTM**](https://github.com/suryansh4424/VM_Scheduler-CloudSim/blob/main/Phase%202/Modeling/03_Bidirectional%20LSTM.ipynb)
- **R² Score**: ~0.61
- **Strengths**:
  - Captures both past and future dependencies in the data.
  - Good for handling complex time series patterns.
- **Weaknesses**:
  - High computational cost and slower training time.
  - No significant accuracy improvement over simpler models.

---

### Conclusion
- **Linear Regression** was selected as the primary model due to its simplicity, faster training time, and comparable performance to more complex models like **GRU** and **Bidirectional LSTM**.


## **3. Results:**
- The models were compared based on their ability to predict the next 10 CPU usage values. The evaluation metrics indicated that the simple **Linear Regression** model provided the best performance, but further optimization is required to improve accuracy.

# [Phase 3](https://github.com/suryansh4424/VM_Scheduler-CloudSim/tree/main/Phase%203): Model Integration

To integrate the predictive models developed in Phase 2 into the VM scheduling framework, enabling real-time workload predictions to optimize resource allocation.

## **1. Framework Selection:**
- **CloudSim** was chosen as the simulation framework for modeling and evaluating VM scheduling in a cloud environment.
- **Eclipse IDE** was used to facilitate seamless integration and debugging of the components.

## **2. Integration Steps:**
### **Model Deployment:**
- The trained **Linear Regression** model was exported as a serialized object and integrated into the CloudSim simulation workflow.
- Predictions were fed into the VM allocation policy to proactively assign resources based on anticipated workloads.

### **Scheduling Algorithm Updates:**
- Enhanced the default VM allocation policy in CloudSim to account for predicted CPU usage values.
- The algorithm dynamically adjusted VM placement and migration strategies based on forecasted demand, aiming to reduce system strain during peak periods.

### **Real-Time Simulation:**
- Simulated real-world scenarios by injecting workload data and observing how the system responded to predicted demands.
- Ensured smooth interaction between the predictive model and the CloudSim framework.

## **3. Results:**
- Successful integration of workload predictions into the VM scheduling process.
- Observed initial improvements in system performance, with more balanced resource utilization compared to heuristic-based methods.

---

# [Phase 4](https://github.com/suryansh4424/VM_Scheduler-CloudSim/tree/main/Phase%204): System Evaluation and Comparison

To evaluate the integrated system's performance and compare AI/ML-based scheduling with traditional heuristic approaches.

## **1. Evaluation Metrics:**
The system was assessed using the following metrics:
- **Resource Utilization**: Percentage of server resources actively in use.
- **Energy Efficiency**: Total energy consumed during the simulation.
- **Scheduling Overhead**: Time and computational resources required for scheduling decisions.
- **Response Time**: Average time taken to handle incoming workloads.

## **2. Benchmarking:**
### **AI/ML-Based Scheduling:**
- Leveraged the predictions from the **Linear Regression** model for VM allocation.
- Proactively adjusted resources based on anticipated demand, minimizing reactive migrations.

### **Heuristic-Based Scheduling:**
- Used static rules and pre-existing information to allocate resources.
- Reactive in nature, often resulting in higher energy consumption and scheduling overhead.

## **3. Results:**
- **AI/ML-Based Approach**:
  - Achieved **10–15% improvement in resource utilization**.
  - Reduced energy consumption by **8–12%** compared to heuristic methods.
  - Lower scheduling overhead due to predictive allocation strategies.

- **Heuristic-Based Approach**:
  - Struggled to adapt to fluctuations in demand, leading to higher reactive costs.
  - Energy consumption and processing times were significantly higher.

## **4. Conclusion:**
- The **AI/ML-based scheduling system** demonstrated superior performance, particularly in dynamic and unpredictable scenarios.
- The proactive approach reduced the need for costly migrations and ensured a more balanced server state, proving the viability of machine learning for optimizing cloud infrastructure.
