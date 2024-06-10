功能列表：
- 更新为es存储
- 反馈机制
- 对话记录

## 界面优化：
- 可以给AI的回答进行打分，好(5)或者不好(0)

d

## 数据存储

有哪些数据？
- 文档元数据 document
- 文档分段 document_segment
- 分段预设问题 document_preset
- 对话记录 chat_record


需要满足哪些功能？
- 检索时，根据preset获取到document
- 对话记录，用户可以给对话打分，记录分数以及问题命中的document和preset


```mermaid
%%{ init: { 'theme': 'dark' } }%%
erDiagram

Document ||..|{ Document_Segment : has
Document ||..|{ Document_Preset : has
Document_Segment ||..|{ Document_Preset : has
Chat_Record ||..|{ Document_Segment : has
Chat_Record ||..|{ Document_Preset : has

Chat_Record {
  String id PK "记录id"
  String question "提问内容"
  String[] segment_id "命中分段ID"
  String[] preset_id "命中预设ID"
  int user_score "用户给的评分"
  int ai_score "AI给的分数"
  String chat_model "回答问题的LLM模型名称"
  date created_time "对话时间"
  String updated_time "记录最后执行操作时间"
}

Document {
  String id PK "文档ID"
  Document_Segment[] segments "分段列表"
  Document_Preset[] presets "预设列表"
  String title "文档标题"
  String url "文档url"
  date created_time "文档写入时间"
  date updated_time "文档更新时间"
}

Document_Segment {
  String id PK "分段ID"
  String content "分段内容"
  dense_vector vector "向量值"
  date created_time "分段写入时间"
  date updated_time "分段更新时间"
}

Document_Preset {
  String id PK "预设ID"
  String content "预设内容"
  String segment_id "分段ID"
  dense_vector vector "向量值"
  date created_time "预设写入时间"
  date updated_time "预设更新时间"
}
```

```json

PUT /document
{
  "mappings": {
    "properties": {
      "id": {
        "type": "keyword"
      },
      "segments": {
        "type": "nested",
        "properties": {
          "id": {
            "type": "keyword"
          }
        }
      },
      "presets": {
        "type": "nested",
        "properties": {
          "id": {
            "type": "keyword"
          }
        }
      },
      "title": {
        "type": "text"
      },
      "content": {
        "type": "text"
      },
      "created_time": {
        "type": "date"
      },
      "updated_time": {
        "type": "date"
      }
    }
  }
}

```

```json
PUT /document_segment
{
  "mappings": {
    "properties": {
      "id": {
        "type": "keyword"
      },
      "content": {
        "type": "text"
      },
      "dense_vector": {
        "type": "dense_vector",
        "dims": 768,  // 这里假设我们使用的模型生成了768维的嵌入向量
        "index": true,  // 启用向量索引，使得可以进行近似最近邻搜索
        "similarity": "cosine"  // 使用余弦相似性作为向量相似度量方法
      },
      "created_time": {
        "type": "date"
      },
      "updated_time": {
        "type": "date"
      }
    }
  }
}

```

```json
PUT /document_preset
{
  "mappings": {
    "properties": {
      "id": {
        "type": "keyword"
      },
      "content": {
        "type": "text"
      },
      "dense_vector": {
        "type": "dense_vector",
        "dims": 768,  // 这里假设我们使用的模型生成了768维的嵌入向量
        "index": true,  // 启用向量索引，使得可以进行近似最近邻搜索
        "similarity": "cosine"  // 使用余弦相似性作为向量相似度量方法
      },
      "created_time": {
        "type": "date"
      },
      "updated_time": {
        "type": "date"
      }
    }
  }
}
```

```json
PUT /chat_record
{
  "mappings": {
    "properties": {
      "id": {
        "type": "keyword"
      },
      "question": {
        "type": "text"
      },
      "answer": {
        "type": "text"
      },
	 "segments": {
        "type": "nested",
        "properties": {
          "id": {
            "type": "keyword"
          }
        }
      },
      "presets": {
        "type": "nested",
        "properties": {
          "id": {
            "type": "keyword"
          }
        }
      },
      "user_score": {
        "type": "integer"
      },
      "model_score": {
        "type": "integer"
      },
      "created_time": {
        "type": "date"
      },
      "updated_time": {
        "type": "date"
      }
    }
  }
}
```
