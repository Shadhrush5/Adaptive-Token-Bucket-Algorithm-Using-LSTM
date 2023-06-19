# Adaptive-Token-Bucket-Algorithm-Using-LSTM
The project focuses on the need for an adaptive token bucket algorithm capable of intelligently allocating tokens based on predicted flow rates in a network. In modern networks, the demand for network resources can vary significantly over time due to factors like peak usage hours or sudden traffic spikes.
Therefore, it becomes crucial to dynamically adjust token allocation to ensure efficient utilization of network resources and maintain a balance between resource availability and demand.

The main questions this project seeks to answer include:
1. How to effectively integrate LSTM-based flow rate prediction into the token bucket algorithm?
2. Can the adaptive token bucket algorithm result in improved token utilization and better resource allocation in a network?

Addressing these questions, this project contributes to existing work by introducing a dynamic and adaptive token allocation mechanism leveraging LSTM-based flow rate prediction.
This approach aims at enhancing resource utilization, optimizing network performance, and addressing challenges posed by varying network traffic patterns.

## Design
The project design involves integration of LSTM-based flow rate prediction into the token bucket algorithm. The hypothesis is that dynamic adjustment of token allocation based on predicted flow rates can lead to better resource utilization. The design includes several key components:

### Token Bucket Algorithm
Implementation of a token bucket algorithm happened with configurable parameters, including capacity, tokens, and rate. The capacity represents the maximum number of tokens the bucket can hold, tokens denote the current number of available tokens, and rate indicates the rate at which tokens get replenished.

### LSTM Model Architecture
An LSTM model for flow rate prediction found use in the project. The input size of the model corresponds to the number of features used for prediction, which in this case is 1 (flow count). The hidden size determines the number of LSTM units in the hidden state, and the output size represents the predicted flow rate.

### Training Process
To train the LSTM model, usage of a dataset containing flow counts over a specific period was necessary. This dataset underwent preprocessing to normalize the flow counts and split into training and validation sets. The LSTM model trained using the Adam optimizer and mean squared error loss. The training process involved iterating over the dataset and updating model parameters to minimize the prediction error.

### Dataset
The dataset "cs448b_ipasn.csv" contains information related to network flows.

1. date: This column represents the date of the network flow data. The dates are in the format "yyyy-mm-dd" and range from 2006-07-01 through 2006-09-30. Each row in the dataset corresponds to a specific date.

2. l_ipn: The "l_ipn" column denotes the local IP address involved in the network flow. It is encoded as an integer ranging from 0 to 9. Each unique value represents a specific local IP address.

3. r_asn: The "r_asn" column represents the remote ASN (Autonomous System Number) associated with the network flow. It is an integer that identifies the remote ISP (Internet Service Provider). Each unique value corresponds to a specific remote ASN.

4. f: The "f" column denotes the flow count, which represents the count of connections or network flows recorded for a particular day. It indicates the volume or intensity of network traffic for each date.

The dataset provides a snapshot of network flow data during the specified time period. It captures information about the dates, local IP addresses, remote ASNs, and flow counts, which can be used for analyzing network traffic patterns, identifying trends, and building predictive models for flow management.

**Link to download**: https://www.kaggle.com/datasets/crawford/computer-network-traffic/download?datasetVersionNumber=1

The design also encompasses incorporation of the LSTM model's predictions into the token bucket algorithm, where predicted flow rates dynamically adjust token requirements for incoming flows. By integrating these components, the aim is to create an adaptive token bucket algorithm that optimizes resource allocation based on real-time flow rate predictions.

**The overall flow of the design is shown in the figure below.**

<img width="440" alt="Screenshot 2023-06-19 at 12 40 54 PM" src="https://github.com/Shadhrush5/Adaptive-Token-Bucket-Algorithm-Using-LSTM/assets/119898772/4eff3777-8512-48c5-a2ce-5236ca34792d">

## Implementation
This project involved implementing a token bucket model with an adaptive component using LSTM. The implementation involved the following steps:

### Data Preparation
The dataset was read from the "cs448b_ipasn.csv" file using pandas. The required columns, including dates, local IPs, remote ASNs, and flow counts were extracted.

### Token Bucket Parameters
Parameters for the token bucket model, such as the bucket capacity, initial token count, and token arrival rate, were defined. These parameters determine the token availability for processing flows.

### LSTM Model and training
An LSTM model was defined using PyTorch. The LSTM model takes the flow rate as input and predicts the
future flow rate based on historical data. It consists of an LSTM layer followed by a fully connected layer.

The LSTM model was trained using the flow rate data. Mean squared error loss was used as the training criterion and the Adam optimizer for model parameter updates. The training was performed for a specified number of epochs.

### Token Bucket Evaluation
After training the LSTM model, the token bucket model was evaluated. For each flow in the dataset, token bucket behavior was simulated by waiting until sufficient tokens were available. The token requirement was adjusted based on the predicted flow rate using the LSTM model. The total tokens used, the total flow count, and the number of matched flow counts were tracked.

## Results and Analysis
The evaluation of the token bucket model yielded the following results:

### Token Utilization
Token utilization was calculated by dividing total tokens used by the expected total tokens for all flows in the dataset. It represents the efficiency of token usage in the token bucket model. In this evaluation, token utilization was measured at 2.49.

### Accuracy
Accuracy was calculated by dividing the number of matched flow counts by the total flow count. It indicates how well the token bucket model predicted the token requirement for each flow. In this evaluation, accuracy was measured at 0.814

These results suggest that the token bucket model with the adaptive component using LSTM performed reasonably well in managing flow token requirements. Token utilization stood at a satisfactory level, and the accuracy of token predictions was relatively high.

The results offer insights into the effectiveness of the token bucket model in handling variable flow rates and adapting to changes using the LSTM-based adaptive component.

<img width="329" alt="Screenshot 2023-06-19 at 12 49 37 PM" src="https://github.com/Shadhrush5/Adaptive-Token-Bucket-Algorithm-Using-LSTM/assets/119898772/a91780c2-c43d-4753-863c-a4ca611c4992">
