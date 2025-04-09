```mermaid
graph TD
    %% 输入数据
    A[输入数据] --> B[IMU数据]
    A[输入数据] --> C[帧数据]

    %% VIO后端处理
    B --> D[前端数据融合]
    C --> D[前端数据融合]

    %% 后端优化
    D --> E[更新轨迹图]
    E --> F[视觉-IMU融合]
    F --> G[优化因子构建]
    G --> H[使用Ceres进行优化]
    H --> I[优化后姿态估计]

    %% 位姿收敛检查
    I --> J{VIO收敛?}
    J -->|Yes| K[伪造世界差分 (如果需要)]
    J -->|Yes| L[执行后处理]
    J -->|Yes| M[更新IMU估计器状态]

    %% 输出结果
    L --> N[输出回调]
    M --> N[输出回调]
    N --> O[数据转储 (如果启用)]

    %% 调试信息
    J -->|No| P[输出调试信息]
    P --> Q[返回VIO结果或调试信息]

    %% 数据存储
    O --> Q
    K --> Q
    L --> Q
    H --> Q

    style A fill:#ffcc00
    style B fill:#ffcc00
    style C fill:#ffcc00
    style D fill:#ffcc00
    style E fill:#ccccff
    style F fill:#ccccff
    style G fill:#ccccff
    style H fill:#ccccff
    style I fill:#ccccff
    style J fill:#ffcc00
    style K fill:#ccccff
    style L fill:#ccccff
    style M fill:#ccccff
    style N fill:#ccccff
    style O fill:#ccccff
    style P fill:#ccccff
    style Q fill:#ffcc00
```
