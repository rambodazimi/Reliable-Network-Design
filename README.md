# Reliable-Network-Design

**Project Description**

The project requires developing a program for designing communication networks between cities. Given the number of cities and characteristics of communication links (cost and reliability), the objective is to construct a network that maximizes reliability within a specified cost constraint.

The program should have two versions: one using **exhaustive enumeration** and the other using an **efficient algorithm**. The exhaustive enumeration method explores all possible network designs, while the efficient algorithm aims to find the optimal solution more quickly.

The program should accept input files specifying the number of cities, costs of inter-city connections, and reliabilities of inter-city connections. Input files for 4, 5, and 6 cities are provided, and the program should run on all three inputs.

## Exhaustive Enumeration

**Implementation**

1.   Read the input text file, extract information, and store to their corresponding variables (*N, reliability_matrix, cost_matrix*). To do so, we have implemented a function called *read_numbers_from_file()* which takes a filename as input, reads the file line by line, ignores lines starting with # (comments), extracts N from the first line, reads the remaining numbers into a list, and finally stores the values in their corresponding variables.

2.   Determine all possible network combinations by generating binary numbers with *N*(N-1)/2* bits. Given N nodes, we can have *2^(N*(N-1)/2)* possible combinations. Therefore, a binary number with that number of digits could cover all possible combinations. We do so by implementing the *generate_binary_numbers()* function. We store all combinations in the *binary_numbers* list.

3. Not all possible combinations are feasible. For example, some combinations do not result in a connected network. To eliminate these combinations, we check whether the created network is connected or not. First, we convert each binary number (representing an *edge list*) into an *adjacency list* by calling the function *binary_to_adjacency()*. This function returns a list called *adj_matrix*, which is then used as input for another function named *is_connected()*. The is_connected() function runs the *Depth-First Search* (DFS) algorithm to determine whether the connected components can traverse all the nodes within the network or not.

4. We iterate over all possible combinations (*binary_numbers*) and eliminate ones that are not connected, and store the remaining to another list called *connected_numbers*.

5. We further eliminate combinations that exceed the cost limit. Given an integer number *cost_limit*, we calculate the total cost of the network using the *calculate_total_cost()* function. If the calculated cost exceeds the cost limit, we remove the combination from the list. This is achieved by iterating over each digit of each remaining binary number, adding the corresponding cost if the digit is '1'. The remaining combinations are then stored in a new list called *feasible_numbers*.

6. Now that we have a set of all possible networks that are both connected and do not exceed the cost limit, represented by their binary numbers (feasible_numbers), we start calculating the reliability of each network in order to find the highest reliability. To do so, we implement the following functions:

*   *calculate_single_reliability()*: Given a network represented by its binary number, we calculate the reliability by multiplying the edges that are connected in the graph. This function is used only when our network is a spanning tree (with no redundancy), so that the total reliability is a simple multiplication of all edge reliabilities.

*   *calculate_reliability()*: Given a network represented by its binary number, we calculate the reliability by considering redundancies as well. If there's only one redundancy (i.e., the number of edges = N), we use *generate_variations()* to generate any possible sub-network from that network that is still possible. By combining all those generated sub-networks and summing up the reliability values, we calculate the total reliability of that network with one redundancy.

*   *generate_variations()*: Given a network (represented by its binary edge list), generate all possible sub-networks with 1 edge less.

*   *generate_variations_all()*: Given a network represented by its binary edge list, we aim to generate all possible sub-networks with two or more edges removed. We achieve this by recursively calling the function on each generated variation until we have combined all possible sub-networks while respecting the connectivity constraint. Then, we flatten the list, remove any duplicates, and return the final result.

7. We store the calculated reliabilities in a list named *reliabilities*.

8. We find the highest reliability by sorting the reliabilities list and returning the first element.

9. Finally, we print important results for the network design.

10. For the interesting feature, we implement a simple GUI representation of the selected newrork graph with the highest reliability.

## Efficient Algorithm
to be completed

# Results

### 4-city

#### Cost Limit: 50
![4-50](https://i.ibb.co/z4mBZdc/4-50.png)
![graph](https://i.ibb.co/S7bzrzw/1.png)

#### Cost Limit: 60
![4-60](https://i.ibb.co/bFWbwsK/4-60.png)
![graph](https://i.ibb.co/z26Yp1B/2.png)

### 5-city

#### Cost Limit: 60
![5-60](https://i.ibb.co/YcRdKTk/5-60.png)
![graph](https://i.ibb.co/Tv6xbkD/3.png)

#### Cost Limit: 70
![5-70](https://i.ibb.co/JBH8hvS/5-70.png)
![graph](https://i.ibb.co/NNMSSrG/4.png)

### 6-city

#### Cost Limit: 65
![6-65](https://i.ibb.co/s21PLk5/6-65.png)
![graph](https://i.ibb.co/W2DyZ6T/5.png)

#### Cost Limit: 85
![6-85](https://i.ibb.co/f8NPvvW/6-85.png)
![graph](https://i.ibb.co/sPkZNRz/6.png)

## Efficient Algorithm

### 4-city
#### Cost Limit: 50
<img width="545" alt="4-50 log" src="https://github.com/rambodazimi/Reliable-Network-Design/assets/60024749/e182e4a3-fd48-4c9a-92d0-a73d30a6e0eb">
<img width="355" alt="4-50 graph" src="https://github.com/rambodazimi/Reliable-Network-Design/assets/60024749/95cf1499-4b40-400d-94e4-654fda2c5352">

#### Cost Limit: 60
<img width="545" alt="4-60 log" src="https://github.com/rambodazimi/Reliable-Network-Design/assets/60024749/0cc730a4-97df-42fe-85d8-54a5d927e69b">
<img width="358" alt="4-60 graph" src="https://github.com/rambodazimi/Reliable-Network-Design/assets/60024749/18d35816-b421-4c5a-8305-7a22ac45f1b0">

### 5-city

#### Cost Limit: 60
<img width="549" alt="5-60 log" src="https://github.com/rambodazimi/Reliable-Network-Design/assets/60024749/4685dc92-fbb6-46cc-9672-3bc29ae4fcc7">
<img width="365" alt="5-60 graph" src="https://github.com/rambodazimi/Reliable-Network-Design/assets/60024749/4db7f091-0a8a-426b-962f-8f278db06eb8">

#### Cost Limit: 70
<img width="559" alt="5-70 log" src="https://github.com/rambodazimi/Reliable-Network-Design/assets/60024749/b22cbc0e-b19e-4556-97ad-b46e1fefe85b">
<img width="377" alt="5-70 graph" src="https://github.com/rambodazimi/Reliable-Network-Design/assets/60024749/29e1369e-74c9-4484-a3bc-24d3874d0608">

### 6-city

#### Cost Limit: 65
<img width="547" alt="6-65 log" src="https://github.com/rambodazimi/Reliable-Network-Design/assets/60024749/6908cf5f-fa2b-43c5-a805-2820570133de">
<img width="375" alt="6-65 graph" src="https://github.com/rambodazimi/Reliable-Network-Design/assets/60024749/560041db-4174-4497-8062-4cd05d80cafd">

#### Cost Limit: 85
<img width="548" alt="6-85 log" src="https://github.com/rambodazimi/Reliable-Network-Design/assets/60024749/267c1f40-2d07-4775-a2ad-80dc17a4e0e1">
<img width="368" alt="6-85 graph" src="https://github.com/rambodazimi/Reliable-Network-Design/assets/60024749/ef46f313-72b9-4f6c-9083-b41c5b742fbf">

# Time Comparison
![timer](https://i.ibb.co/fG9W571/Screenshot-2024-04-07-at-1-34-16-AM.png)
