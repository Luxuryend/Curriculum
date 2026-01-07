#### 1. 初始化样本权重
$D_1 = (w_{11}, w_{12}, ..., w_{1N}), \quad w_{1i} = \frac{1}{N}, \quad i=1,2,...,N$
（N为样本总数，初始时所有样本权重相等）

#### 2. 计算基分类器的误差率
$\epsilon_m = P(G_m(x_i) \neq y_i) = \sum_{i=1}^{N} w_{mi} I(G_m(x_i) \neq y_i)$
（$I(\cdot)$为指示函数，$G_m(x)$为第m个基分类器，$\epsilon_m$为第m轮分类器的加权误差率）

#### 3. 计算基分类器的权重
$\alpha_m = \frac{1}{2} \ln \frac{1 - \epsilon_m}{\epsilon_m}$
（$\alpha_m$表示第m个基分类器在最终集成中的重要性，误差越小权重越大）

#### 4. 更新样本权重
$D_{m+1} = (w_{m+1,1}, w_{m+1,2}, ..., w_{m+1,N})$
$w_{m+1,i} = \frac{w_{mi}}{Z_m} \exp(-\alpha_m y_i G_m(x_i)), \quad i=1,2,...,N$
（$Z_m = \sum_{i=1}^{N} w_{mi} \exp(-\alpha_m y_i G_m(x_i))$ 为归一化因子，保证权重和为1）

#### 5. 构建最终集成分类器
$G(x) = \text{sign}\left( \sum_{m=1}^{M} \alpha_m G_m(x) \right)$
（$\text{sign}(\cdot)$为符号函数，M为基分类器总数，最终输出所有基分类器的加权投票结果）
