## list去重
```
 ArrayList<VolumeMountQuery> list = volumeMountList.stream()
 .collect(Collectors.collectingAndThen(Collectors.toCollection(() -> new TreeSet<>(Comparator.comparing(VolumeMountQuery::getName))), ArrayList::new));
```
## 生成聚合map
```
Map<String, Set<String>> permissionRoleMap = new HashMap<>();
        Map<String, String> roleCodeMap = roleList.stream()
                .collect(Collectors.toMap(RoleDO::getId, RoleDO::getRoleCode));
        Map<String, Set<String>> groupRoleCodeMap = roleGroups.stream().collect(
                Collectors.groupingBy(RolePermissionGroupDO::getPermissionGroupId,
                        Collectors.mapping(t -> roleCodeMap.get(t.getRoleId()),Collectors.toSet())));
        groupRelations.stream().collect(Collectors.groupingBy(PermissionGroupRelationDO::getPermissionId,
                Collectors.mapping(PermissionGroupRelationDO::getPermissionGroupId,Collectors.toSet())))
                .forEach((k,v) ->{
            Set<String> reduce = v.stream().map(groupRoleCodeMap::get).reduce(new HashSet<>(), (a, b) -> {
                if(b!=null){
                    a.addAll(b);
                }
                return a;
            });
            permissionRoleMap.put(k,reduce);
        });
```
