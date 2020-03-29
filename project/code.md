
#### 任务管理
1. 代码逗号拼接

```
/**
    * 返回文书列表
    *
    * @param pageNumber
    * @param pageSize
    * @return
    */
   @Override
   public Map<String, Object> getDocList(Integer pageNum, Integer pageSize) {

       String sql = "select t.wsmc, t.wscode, t.wsbm," +
           " to_char(t.inittime,'yyyy-mm-dd hh24:mi:ss') inittime," +
           " to_char(t.updatetime,'yyyy-mm-dd hh24:mi:ss') updatetime," +
           " t.state" +
           " from portal.docmanagement t";
       Map<String,Object> queryPageBySQL = PageInfoUtil.queryPageBySQL(baseDao,sql,pageNum,pageSize);
       //获取关键词
       Map<String,Object> keyWordMap = getKeyWords();
       List<Map<String,Object>> mapAll = (List<Map<String, Object>>) queryPageBySQL.get("t");
       //添加关键词
       for(Map<String,Object> map:mapAll){
           System.out.println("wscode：" + map.get("wscode"));
           if(keyWordMap.containsKey(map.get("wscode"))){
               map.put("keyword",keyWordMap.get(map.get("wscode")));
           }else{
               map.put("keyword",null);
           }
       }
       queryPageBySQL.put("t",mapAll);
       return queryPageBySQL;
   }
/**
    * 获取关键词
    * @return
    */
   public Map<String,Object> getKeyWords(){
       String sql = "select k.wscode, k.gjcmc " +
               " from portal.docmanagementkeyword k" +
               " where k.gjcmc is not null";
       List<Map<String,Object>> keyList = baseDao.queryBySQL(sql);
       //存储<文书编码,关键词>
       Map<String,Object> keyWordsMap = new LinkedHashMap<>();
       String keyCode = "wscode"; //文书编码字段名
       String keyGjc = "gjcmc" ; //关键词字段名
       //遍历 将相同文书编码的关键词用逗号连接
       for(Map<String,Object> map:keyList){
           //获取文书编码
           String key = String.valueOf(map.get(keyCode));
           //相同的文书编码值 则拼接关键词
           if(keyWordsMap.containsKey(key))
           {
               keyWordsMap.put(key, keyWordsMap.get(key)+","+map.get(keyGjc));
           }else{
               keyWordsMap.put(key,map.get(keyGjc));
           }
       }
       return keyWordsMap;
   }

```

2，遍历List<Map<String,Object>>
```
public class Test {
    public static void main(String[] args) {

        List<Map<String, Object>> listMaps = new ArrayList<Map<String, Object>>();

        Map<String, Object> map1 = new HashMap<String, Object>();
        map1.put("1", "a");
        map1.put("2", "b");
        map1.put("3", "c");
        listMaps.add(map1);

        Map<String, Object> map2 = new HashMap<String, Object>();
        map2.put("11", "aa");
        map2.put("22", "bb");
        map2.put("33", "cc");
        listMaps.add(map2);

        for (Map<String, Object> map : listMaps) {
            for (String s : map.keySet()) {
                System.out.print(map.get(s) + "  ");
            }
        }
        System.out.println();
        System.out.println("========================");
        for (int i = 0; i < listMaps.size(); i++) {
            Map<String, Object> map = listMaps.get(i);
            Iterator iterator = map.keySet().iterator();
            while (iterator.hasNext()) {
                String string = (String) iterator.next();
                System.out.println(map.get(string));
            }
        }
        System.out.println("++++++++++++++++++++++++++++");
        for (Map<String, Object> map : listMaps) {
            for (Map.Entry<String, Object> m : map.entrySet()) {
                System.out.print(m.getKey() + "    ");
                System.out.println(m.getValue());
            }
        }
        System.out.println("-----------------------------");
    }

}


打印的结果：

c  b  a  bb  cc  aa  
========================
c
b
a
bb
cc
aa
++++++++++++++++++++++++++++
   c
   b
   a
   bb
   cc
   aa
-----------------------------
```
