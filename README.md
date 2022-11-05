# -1260
C언어 백준 1260 : DFS와 BFS
#include <stdio.h>
#include <stdlib.h>
#define MAX_VERTICES 1001

typedef struct Graph{
	int n;
	int adj_mat[MAX_VERTICES][MAX_VERTICES];
}Graph;

void init(Graph *g) {
	g->n = 0;
	for(int i=0;i<MAX_VERTICES;i++)
		for(int j=0;j<MAX_VERTICES;j++)
			g->adj_mat[i][j]=0;
}

void insert_vertex(Graph *g, int n) {
	for(int i=0;i<=n;i++)
		g->n++;
}

void insert_edge(Graph *g, int start, int end) {
	g->adj_mat[start][end]=1;
	g->adj_mat[end][start]=1;
}

int dfs_visited[MAX_VERTICES];
void dfs_mat(Graph *g,int v) {
	dfs_visited[v]=1;
	printf("%d ",v);
	for(int i=0;i<g->n;i++) {
		if(g->adj_mat[v][i]&&!dfs_visited[i]) {
			dfs_mat(g,i);
		}
	}
}

int queue[MAX_VERTICES];
int bfs_visited[MAX_VERTICES];
void bfs_mat(Graph *g,int v) {
	bfs_visited[v]=1;
	printf("%d ",v);
	int front,rear;
	front = rear = 0;
	queue[0]=v;
	rear++;
	while(front<rear) {
		v=queue[front];
		front++;
		for(int i=0;i<g->n;i++) {
			if(g->adj_mat[v][i]&&!bfs_visited[i]) {
				bfs_visited[i]=1;
				printf("%d ",i);
				queue[rear]=i;
				rear++;
			}
		}
	}
	
}

int main(int argc, char* argv[]) {
	int n, m, v;
	scanf("%d %d %d",&n,&m,&v);
	Graph *g;
	g=(Graph *)malloc(sizeof(Graph));
	init(g);
		
	insert_vertex(g,n);
	
	for(int i=0;i<m;i++) {
		int start,end;
		scanf("%d %d",&start,&end);
		insert_edge(g,start,end);
	}
	
	dfs_mat(g,v);
	printf("\n");
	bfs_mat(g,v);
}
