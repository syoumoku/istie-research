# iSite v3.2 SKILL（主规范）

## 文档定位
本文件为 iSite 主规范，保留完整规则，不因追求简洁而删除关键执行信息。
后续如需压缩，只能新增速查版或附表，不得直接删改本文件中的核心规则。

## 五模块 SOP
1. 扫描范围定义模块
2. 扫楼与实体识别模块
3. 证据加工与标准化模块
4. 价值评估模块
5. 呈现与交付模块

## 1. 扫描范围定义模块
### 目标
明确本轮扫描的国家、城市、场景、数据源、口径、输出结构。

### 必做项
- 明确国家范围、核心城市池、次级城市池
- 明确场景池
- 明确数据源优先级
- 明确纳入/排除规则
- 明确输出字段与分层口径

### 场景池
- 机场
- 体育场馆
- 购物中心 / 大型零售综合体
- 会展中心 / 展览中心 / 会议中心
- 酒店 / 高端酒店集群
- 办公楼 / 总部楼宇 / 总部园区
- 医院 / 医疗园区
- 城市综合体 / mixed-use
- 轨交枢纽型商业体
- 文旅综合体 / 城市地标型物业

### 数据源优先级
1. 官方或准官方来源
2. 地理底图与结构化知识源
3. 行业协会、场馆/商场/酒店/会展官方页面
4. 高可信公开目录与百科
5. 其他公开来源

### 输出口径
- 不固定每国输出数量
- 先建立全量 universe，再按得分和证据等级分层输出
- 输出必须保留高优、候选、观察、排除四层

## 2. 扫楼与实体识别模块
### 目标
把楼尽可能全地找出来，并确认物业点是谁、在哪、属于什么场景。

### 核心任务
- 多源找楼
- 名称扩展
- 实体去重
- 重名消歧
- 城市归属确认
- 经纬度确认
- 场景初分类
- 形成 raw candidate universe

### 执行要求
- 本模块不做高价值淘汰，只做识别和清洗
- 尽量保留长名单
- 不得因资料不全直接删除疑似高价值点位
- 名称、城市、坐标、场景至少完成两项强校验
- 无法完成强校验的，保留在 raw candidate universe，并标记待核

### 输出
- raw candidate universe
- validated candidate set
- 去重映射表
- 重名冲突记录表
- 场景初分类表

## 3. 证据加工与标准化模块
### 目标
将原始公开信息加工为可进入评分引擎的标准化证据对象。

### 标准化证据槽位
#### A. 实体与分类类
- entity_resolution_basis
- classification_basis
- country
- city
- district
- scenario
- sub_scenario
- single_building_or_campus

#### B. 客观规模类
- primary_objective_metric_name
- primary_objective_metric_value
- secondary_objective_metric_name
- secondary_objective_metric_value
- national_rank_estimate
- city_rank_estimate

#### C. 用户与业态类
- tenant_mix
- luxury_presence
- business_presence
- international_presence
- visitor_mix
- service_tier

#### D. 品牌与门户类
- brand_tier
- public_recognition
- gateway_role
- landmark_role
- demonstration_effect

#### E. 空间形态类
- tower_count
- campus_layout
- underground_presence
- bridge_podium_presence
- public_space_complexity
- hotspot_diversity

#### F. 证据质量类
- proxy_basis_standardized
- proxy_level
- source_list
- source_time
- conflict_notes
- evidence_grade
- hard_metric_completeness
- multi_source_check
- cap_reason

### 证据类型
- 直接证据：物业点自身公开数据
- 间接证据：同一实体关联公开数据
- 类推证据：同类物业、城市级、国家级 proxy
- 判断性推断：基于证据的分析结论

### proxy basis 标准层级
1. 物业级直接证据
2. 同类物业 proxy
3. 城市级 proxy
4. 国家级 proxy

### 证据约束层
以下字段不直接进入主评分：
- evidence_grade
- proxy_level
- hard_metric_completeness
- multi_source_check
- cap_reason

### 输出
- 标准化证据表
- proxy basis 表
- source traceability 表
- conflict 表
- evidence grade 表
- 证据—评分映射表

## 4. 价值评估模块
### 五维主评分
- PV：物业价值分
- CM：容量模型分
- PU：高端用户分
- BR：口碑 / 品牌 / 门户分
- CX：空间复杂度分

Total Score = 20 × (0.24×PV + 0.28×CM + 0.18×PU + 0.18×BR + 0.12×CX)

### 证据—评分映射原则
- 地位、规模、区位类证据 → PV
- 场景规模、峰值、驻留、聚集、敏感度类证据 → CM
- 用户结构、消费能力、商务与国际化类证据 → PU
- 品牌等级、口碑、门户、示范效应类证据 → BR
- 建筑形态、楼栋结构、地下连桥、热点分布类证据 → CX
- evidence_grade、proxy_level、hard_metric_completeness、multi_source_check、cap_reason → 仅用于封顶与分层，不用于加分

### PU 与 BR 边界
- PU 只评估用户结构，不直接评估品牌知名度
- BR 只评估认知价值和外溢效应，不直接评估用户支付能力
- 同一条证据按其主要回答的问题归属，不得双重喂分

### 输出要求
每个物业点必须输出：
- 五维分项分
- 容量模型五子项分
- 关键客观指标
- proxy 层级
- evidence_grade
- 总分
- 扣分/封顶原因

## 5. 呈现与交付模块
### 分析型输出
- Raw candidates 长表
- 标准化证据表
- 评分拆解表
- proxy basis 表
- excluded / downgraded 表

### 管理型输出
- 国家摘要表
- 城市摘要表
- 高价值物业清单
- 洞察卡
- Excel 主交付
- PPT 汇报版

### Excel 最低要求
- country
- city
- property_name
- scenario
- key_objective_metric
- PV
- CM
- PU
- BR
- CX
- total_score
- evidence_grade
- proxy_basis_standardized
- source_list
- notes

### PPT 最低要求
- 国家级概览
- 场景分布
- 高价值物业分层
- 证据链示例
- 白盒评分示例
- 关键高分物业点
- 风险与数据缺口

## 标准 SOP
1. 扫描范围定义
2. 扫楼与实体识别
3. 证据加工与标准化
4. 价值评估
5. 呈现与交付
