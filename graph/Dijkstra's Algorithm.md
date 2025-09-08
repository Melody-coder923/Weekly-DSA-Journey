"""
import heapq

# 1. 邻接表表示图（Adjacency List）
class Graph:
    def __init__(self, num_nodes):
        # 初始化邻接表
        self.num_nodes = num_nodes
        self.adj_list = {i: [] for i in range(num_nodes)}

    # 添加一条边：从 node1 到 node2，权重为 weight
    def add_edge(self, node1, node2, weight):
        self.adj_list[node1].append((node2, weight))
        self.adj_list[node2].append((node1, weight))  # 如果是无向图，反向也需要添加

    def __repr__(self):
        return str(self.adj_list)

# 2. 迪杰斯特拉算法（Dijkstra's Algorithm）
def dijkstra(graph, start):
    # 1. 初始化距离字典，源点到自己为 0，其他节点为无穷大
    distances = {node: float('inf') for node in range(graph.num_nodes)}
    distances[start] = 0

    # 2. 使用优先队列（最小堆）来存储待处理的节点
    # heapq 中的每个元素是 (当前距离, 节点)
    pq = [(0, start)]  # 以 (距离, 节点) 的形式存入优先队列

    while pq:
        # 3. 获取当前最小距离的节点
        current_distance, current_node = heapq.heappop(pq)

        # 如果该节点的距离已经大于当前的最短路径，则跳过
        if current_distance > distances[current_node]:
            continue

        # 4. 更新邻接节点的距离
        for neighbor, weight in graph.adj_list[current_node]:
            distance = current_distance + weight

            # 如果通过当前节点的路径更短，则更新最短路径并将邻居节点加入队列
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                heapq.heappush(pq, (distance, neighbor))

    return distances
"""
