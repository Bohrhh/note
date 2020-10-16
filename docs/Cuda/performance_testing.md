# nvprof

#### 配置：除去sudo权限
1. 编辑 `/etc/modprobe.d/profile.conf`，加入 `options nvidia "NVreg_RestrictProfilingToAdminUsers=0"`
2. 重启计算机

#### 简单的命令
1. 检测 **warp divergence**  
`nvprof --metrics branch_efficiency ./example`

2. 