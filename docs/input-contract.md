# 原始资料约定

坐标限定为分段矩形参数面，无三维建模要求。geometry.jsonl 将 segment 内本地 u(mm),v(degree) 映射为 physical_piece 上 s_mm=u*scale+offset_s,theta=(v+offset_angle)%360；有效范围左闭右开。scanner_grid.jsonl 给出网格原点及步长。这里定义格式转换，不规定目标存储结构。
scans.parquet 每行是矩形单元观测，u0/u1/v0/v1、amplitude、quality、scan；scan_runs.jsonl 引用 geometry/calibration/grid，含 taken_at/method/resolution。calibration.csv 的 valid 标志与增益决定信号幅值。
repairs.jsonl 给出 piece/s0/s1/theta0/theta1/completed_at/material；requirements.csv 给材料所需方法、最大分辨率、最大幅值。closure_requests.jsonl 为签发请求。角度theta0>theta1表示跨零度，等值仅为零面积。
coordinates=grid时u/v字段为网格行列边界索引；local时为毫米和度。校准gain乘原amplitude。同calibration后续通知替代有效标志但不改原扫描字节。

所有名称与数值均为本地合成数据，不代表真实企业、监管结论或生态调查。data/catalog.json 保存文件哈希、原始行数与列；data/updates/ 为后到修订资料，可独立接收。JSON null 表示尚无该值，不与数值零等同；CSV保留原字符串，金额和数量应按十进制解释。来源身份相同且内容相同的重送不产生新业务事实，同身份版本不同内容需保留争议，除明确替代关系外不按到达顺序判定权威。

geometry省略revision为1；同geometry较大revision是原几何解释的勘误，适用于其有效期间的历史扫描，不改变采集时间。
