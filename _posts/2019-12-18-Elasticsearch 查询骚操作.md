## 平均值
<details>
<summary>求字段 field1 符合条件的值的平均值</summary>
  
<pre><code>
{
  "query": {
    "bool": {
      "filter": []
    }
  },
  "size": 0,
  "aggs": {
    "name1": {
      "filter": {
        "range": {
          "fieldName1": {
            "gte": 0,
            "lte": 10,
          }
        }
      },
      "aggs": {
        "name1.1": {
          "avg": {
            "field": "fieldName1"
          }
        }
      }
    },
    "responseOverTime": {
      "date_histogram": {
        "field": "时间字段",
        "extended_bounds": {
          "min": 时间范围begin,
          "max": 时间范围end
        },
        "interval": "1000h"
      },
      "aggs": {
        "name2": {
          "avg": {
            "field": "fieldName2"
          }
        },
        "name3": {
          "avg": {
            "field": "fieldName3"
          }
        }
      }
    }
  }
}
</code></pre>
</details>

# 持续完善
