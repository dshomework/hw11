# Nothing much to say...

## Prim
1. 从某一点出发（随便选，假设选点0）
2. 找离出发点最近的点，记录下来并做相关计算
3. 在未找过的点集中找离已找过的点最近的点，记录下来并做相关计算
4. 重复 step 3 直至所有点都已找过。

	memset(v, 0, sizeof(v));
	memset(d, 0, sizeof(d));
	src = 0;
	
	// Initial fringe is {src}
	v[src] = true;
	// d[i] means the shortest edge from fringe to Node_i.
	for (i = 0 .. N) 
	    d[i] = a[src][i];
	
	int sum = 0;
	for (i = 1 .. N) {
	    int min = LONG_MAX;
	    int p = -1;
	    p = get_nearest_unvisited_node();
	    // Add p into fringe
	    v[p] = true;
	    sum += d[p];
	    
	    // update the shortest edge from fringe to unvisited nodes, since fringe has been changed.
	    update_d_by_p();        
	}

## Kruskal
1. 将所有边从小到大排序，然后开始遍历边
2. 对于当前的边，如果边两头的两个节点位于同一个并查集，则continue跳过
3. 对于当前的边，如果边两头的两个节点不在同一个集合，则可认为该边必然是MST中的边。记录下边，并将边的两个节点的集合合并。
4. 重复step 2&3 ，直至成功记录了 N - 1 条边。


	sort(edges);
	
	int sum = 0;
	int k = 0;
	for (i = 0 .. edges.length)
	    if (k == N - 1)
	        break;
	
	    e = edges[i];
	    if (sameSet(e.x, e.y))
	        continue;
	
	    mergeSet(set(e.x), set(e.y));
	    k++;
	    sum += e.len;
