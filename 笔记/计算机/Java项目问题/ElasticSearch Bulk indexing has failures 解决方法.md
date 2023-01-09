

启动配置有ElasticSearch参数的java jar 应用是报：

# org.springframework.data.elasticsearch.ElasticsearchException: Bulk indexing has failures

ES新节点的数据目录data存储空间不足

1.提供足够的存储空间供数据写入，如需在配置文件中更改ES数据存储目录，注意重启ES  
2.放开索引只读设置，在Kibana的开发工具Dev Tools中执行

![](https://img2020.cnblogs.com/blog/1346983/202107/1346983-20210701113524740-620736193.png)

PUT _settings  
{  
  "index.blocks.read_only_allow_delete": null

}

返回如下：

{

"acknowledged":true

}

--------------------------------

failed to load elasticsearch nodes : org.elasticsearch.cluster.block.ClusterBlockException: blocked by: [FORBIDDEN/12/index read-only / allow delete (api)];  
解决办法：  
curl -XPUT -H "Content-Type: application/json" http://master:9200/_all/_settings -d '{"index.blocks.read_only_allow_delete": null}'