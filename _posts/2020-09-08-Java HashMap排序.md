## 获取top5

```code
  List<Map.Entry<String, Double>> list = new ArrayList<Map.Entry<String, Double>>(m.entrySet());
  //使用Collections工具类对list进行排序
  Collections.sort(list, new Comparator<Map.Entry<String, Double>>() {
      @Override
      public int compare(Map.Entry<String, Double> o1, Map.Entry<String, Double> o2) {
          // TODO Auto-generated method stub
          //按Entry里面的value降序排序
          return o2.getValue().compareTo(o1.getValue());
          //按Entry里面的value升序排序
          //return o1.getValue().compareTo(o2.getValue());

      }

  });
  /**

   *将按value排好序的Entry放入map中
   **/
  Map<String, Object> lhm = new LinkedHashMap<String, Object>();
  int num = 0;
  for(Map.Entry<String, Double> temp:list){
      if (num > 4){
          break;
      }
      lhm.put(temp.getKey(), temp.getValue());
      num++;
  }
```
