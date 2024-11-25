import json


def match_and_splice_objects(objects_list, key_to_match, keywords):
    """
    对给定的对象列表，匹配对象中指定属性的值是否包含关键词，匹配后进行二次拼接，返回可JSON解析的结果

    :param objects_list: 包含对象（以字典形式表示）的列表
    :param key_to_match: 需要匹配的对象属性的键名
    :param keywords: 要匹配的关键词列表
    :return: 可JSON解析的结果，以字典形式存储，键为关键词，值为匹配该关键词的对象拼接后的新字典列表
    """
    result_dict = {}
    for keyword in keywords:
        result_dict[keyword] = []
        for obj in objects_list:
            if key_to_match in obj and keyword in obj[key_to_match]:
                # 进行二次拼接，这里假设给匹配的对象添加一个新属性 '拼接说明'
                obj['拼接说明'] = "匹配到关键词 " + keyword + " 的对象"
                result_dict[keyword].append(obj)
    return result_dict


if __name__ == "__main__":
    # 模拟的对象列表，实际中可以从数据库查询结果等获取
    objects_list = [
        {"name": "产品A", "description": "这是包含苹果的产品描述"},
        {"name": "产品B", "description": "这是普通的产品描述"},
        {"name": "产品C", "description": "这是包含香蕉的产品描述"}
    ]
    key_to_match = "description"
    keywords = ["苹果", "香蕉"]
    final_result = match_and_splice_objects(objects_list, key_to_match, keywords)
    print(json.dumps(final_result, ensure_ascii=False, indent=4))
