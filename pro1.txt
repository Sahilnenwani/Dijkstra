#import numpy as np
class dijkstra:
    def function(self, edges, n,sor,ds):
        self.distance = [float('inf') for i in range(n)]

        self.visited=[False for i in range(n)]
        self.visitedindex=self.visited
        #self.visited = np.array([False for i in range(n)])
        #self.visited=self.visited.astype('bool')
        #for i in range (n):
            # self.distance[i] = float('inf')
            # self.visited = False
        self.distance[sor] = 0
        for i in range(n - 1):

            self.minvertex = self.findminvertex(self.distance, self.visited, n)
            self.visited[self.minvertex] = True
            for j in range(n):
                if (self.edges[self.minvertex][j] != 0 and self.visited[j]==False):
                    self.dist = self.distance[self.minvertex] + self.edges[self.minvertex][j];
                    if (self.dist < self.distance[j]):
                        self.distance[j] = self.dist;
        print("vertices     shortest path")
        for i in range(n):
            print( str(i) + "              " + str(self.distance[i]))
        print(f"from source {sor} ---->{ds} the shotest path is {self.distance[ds]}")
    def findminvertex(self, distance, visited, n) :
        minvertex = - 1
        for i in range(n):
            if (  self.visited[i]==False and (minvertex == -1 or self.distance[i] < self.distance[minvertex])):
                        minvertex = i;
            else:
                continue
        return minvertex

    def main(self):
        print("Make graph like this")
        print("""    
                            5
                       (1)-------(3) 
                      / |       /  |
                   4 /  |      /   |    
                    /   |     /    |   4
                (0)    2|   5/     |
                    \   |   /      |
                   8 \  |  /       |
                      \ | /        |
                       (2)-------(4)
                            9
         
         """)
        print("find the shortest path between nodes")
        print("enter total number of vertices and edges ")
        self.n = int(input(" enter num of vertixes: "))
        self.e = int(input(" enter num of  edges: "))
        self.edges = [[0 for i in range(self.n)] for j in range(self.n)]


        # for i in range(self.n):
        #    for j in range(self.n):
        #
        #      self.edges[i][j] = 0
        for i in range(self.n):
           self.edges[i] = [i for i in range(self.n+1)]
           for j in range(self.n):
            self.edges[i][j] = 0
        print("Now enter the first and second vetices and their weigth")
        for i in range(self.e):
            self.f = int(input("enter value of first: "))
            self.s = int(input("enter value of second: "))
            self.weight = int(input("enter value of weigth: "))
            self.edges[self.f][self.s] = self.weight
            self.edges[self.s][self.f] = self.weight
        sour=int(input("Now enter the source vertix"))
        des=int(input("Now enter destination vertix"))
        self.function(self.edges, self.n,sour,des)

dijkstra().main()