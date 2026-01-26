# Map Queries - SQL Code

**Tags:** #code #sql #maps

## Query 1: By Size Category
```sql
SELECT 
    address, net_units, year, 
    latitude, longitude, size_category
FROM map_view
ORDER BY net_units DESC;
```

## Query 2: Recent Projects (2020+)
```sql
SELECT 
    address, net_units, year,
    latitude, longitude,
    year || ' | ' || address || ' | ' || net_units || ' units' as popup_label
FROM map_view
WHERE year >= 2020
ORDER BY year DESC, net_units DESC;
```

## Query 3: Geographic Clustering
```sql
WITH project_clusters AS (
    SELECT 
        p1.address, p1.latitude, p1.longitude,
        p1.net_units, p1.year,
        COUNT(DISTINCT p2.address) - 1 as nearby_projects
    FROM map_view p1
    LEFT JOIN map_view p2 
        ON ABS(p1.latitude - p2.latitude) < 0.005
        AND ABS(p1.longitude - p2.longitude) < 0.005
    GROUP BY p1.address, p1.latitude, p1.longitude, p1.net_units, p1.year
)
SELECT 
    address, latitude, longitude, net_units, year,
    nearby_projects,
    CASE 
        WHEN nearby_projects >= 10 THEN '🏙️ High Density'
        WHEN nearby_projects >= 5 THEN '🏘️ Cluster'
        WHEN nearby_projects >= 2 THEN '🏗️ Multiple'
        ELSE '🏠 Isolated'
    END as cluster_type
FROM project_clusters
ORDER BY nearby_projects DESC;
```

## Query 4: Top 20 Largest
```sql
SELECT 
    address, net_units, year,
    latitude, longitude,
    ROW_NUMBER() OVER (ORDER BY net_units DESC) as rank
FROM map_view
ORDER BY net_units DESC
LIMIT 20;
```

**Last Updated:** 2026-01-09
