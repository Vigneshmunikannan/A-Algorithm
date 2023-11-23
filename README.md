# A-Algorithm

# ALGORITHM

1. Initialize the open list
2. Initialize the closed list
put the starting node on the open
list (you can leave its f at zero)
3. while the open list is not empty
a) find the node with the least f on
the open list, call it "q"
b) pop q off the open list
c) generate q's 8 successors and set their
parents to q
d) for each successor
i) if successor is the goal, stop search
ii) else, compute both g and h for successor


# CODE 

import heapq

def euclidean_distance(point1, point2):
    # Placeholder Euclidean distance heuristic
    return 0

def a_star(graph, start, goal):
    open_set = []
    closed_set = set()

    # Priority queue to store nodes based on their f values
    heapq.heappush(open_set, (0, start))

    g = {point: float('inf') for point in graph}
    g[start] = 0

    parents = {point: None for point in graph}

    while open_set:
        current_cost, current_point = heapq.heappop(open_set)

        if current_point == goal:
            # Reconstruct the path
            path = []
            while current_point is not None:
                path.append(current_point)
                current_point = parents[current_point]
            path.reverse()
            return path

        closed_set.add(current_point)

        for neighbor in graph[current_point]:
            if neighbor in closed_set:
                continue

            tentative_g = g[current_point] + 1  # Assuming all edges have a cost of 1

            if tentative_g < g[neighbor]:
                g[neighbor] = tentative_g
                parents[neighbor] = current_point
                f_value = tentative_g + euclidean_distance(neighbor, goal)
                heapq.heappush(open_set, (f_value, neighbor))

    return None  # No path found

def get_user_input():
    # Get input from the user for points and edges
    graph = {}

    num_points = int(input("Enter the number of points: "))

    for _ in range(num_points):
        point = input("Enter a point label: ")
        graph[point] = []

    num_edges = int(input("Enter the number of edges: "))

    for _ in range(num_edges):
        edge_info = input("Enter edge information (point1 point2): ").split()
        point1, point2 = edge_info[0], edge_info[1]

        graph[point1].append(point2)
        graph[point2].append(point1)

    start_point = input("Enter the start point label: ")
    goal_point = input("Enter the goal point label: ")

    return graph, start_point, goal_point

if __name__ == "__main__":
    user_graph, user_start, user_goal = get_user_input()

    result = a_star(user_graph, user_start, user_goal)

    if result:
        print("Optimal Path:", result)
    else:
        print("No path found.")


# Link to run if this copy paste is not working
https://replit.com/@vigneshm2021csb/A-alogorithm#main.py

# INPUT
Enter the number of points: 4
Enter a point label: A
Enter a point label: B
Enter a point label: C
Enter a point label: D
Enter the number of edges: 5
Enter edge information (point1 point2): A B
Enter edge information (point1 point2): A C
Enter edge information (point1 point2): B C
Enter edge information (point1 point2): B D
Enter edge information (point1 point2): C D
Enter the start point label: A
Enter the goal point label: D

# OUTPUT
Optimal Path: ['A', 'B', 'D']
