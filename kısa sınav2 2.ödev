#include <stdio.h>
#include <stdlib.h>
#include <math.h>

#define N 10
#define EPSILON 2.0
#define MIN_PTS 3

struct point {
    double x, y;
};

struct point dataset[N] = {
    {1, 1},
    {1.5, 2},
    {3, 4},
    {5, 7},
    {3.5, 5},
    {4.5, 5},
    {3.5, 4.5},
    {2.5, 1.5},
    {3.5, 1},
    {4.5, 1.5}
};

struct point neighbors[N][N];

int get_neighbors(int index, double epsilon) {
    int count = 0;
    for (int i = 0; i < N; i++) {
        if (i != index) {
            double distance = sqrt(pow(dataset[i].x - dataset[index].x, 2) + pow(dataset[i].y - dataset[index].y, 2));
            if (distance <= epsilon) {
                neighbors[index][count] = dataset[i];
                count++;
            }
        }
    }
    return count;
}

void expand_cluster(int index, int cluster_id, double epsilon, int min_pts, int* clusters, int* visited) {
    clusters[index] = cluster_id;
    for (int i = 0; i < N; i++) {
        if (visited[i]) continue;
        double distance = sqrt(pow(dataset[i].x - dataset[index].x, 2) + pow(dataset[i].y - dataset[index].y, 2));
        if (distance <= epsilon) {
            visited[i] = 1;
            int neighbor_count = get_neighbors(i, epsilon);
            if (neighbor_count >= min_pts) {
                for (int j = 0; j < neighbor_count; j++) {
                    if (!visited[j]) {
                        neighbors[i][j] = dataset[j];
                    }
                }
            }
            expand_cluster(i, cluster_id, epsilon, min_pts, clusters, visited);
        }
    }
}

int main() {
    int clusters[N];
    int visited[N] = {0};
    int cluster_id = 0;
    
    for (int i = 0; i < N; i++) {
        if (!visited[i]) {
            visited[i] = 1;
            int neighbor_count = get_neighbors(i, EPSILON);
            if (neighbor_count < MIN_PTS) {
                clusters[i] = -1;
            } else {
                cluster_id++;
                expand_cluster(i, cluster_id, EPSILON, MIN_PTS, clusters, visited);
            }
        }
    }
    
    // Sonuçları yazdırma
    for (int i = 0; i < N; i++) {
        printf("Nokta %d, Kume: %d\n", i, clusters[i]);
    }
    
    return 0;
}
