# ARIMA时序模型

1. 数据预处理；
2. Target做log1p转换，降低其偏度和峰度；
3. 提取训练集中store==1$&item==1的数据做分析；
4. 数据做平稳diff处理；
5. 可视化其自相关、偏自相关、季节性、趋势等特征；
6. 根据结果提取ARIMA的参数(7,1,1)，网格搜索结果(8,0,2)，注意这个结果是基于diff1计算的，所以d为0；
7. 基于未diff数据结果如下，最好是801，但是由于测试数据不全，还是取711：

        ARIMA(6, 0, 0) MSE=0.081
        ARIMA(6, 0, 1) MSE=0.073
        ARIMA(6, 0, 2) MSE=0.073
        ARIMA(6, 1, 0) MSE=0.069
        ARIMA(6, 1, 1) MSE=0.068
        ARIMA(6, 1, 2) MSE=0.069
        ARIMA(6, 2, 0) MSE=0.107
        ARIMA(7, 0, 0) MSE=0.068
        ARIMA(7, 0, 1) MSE=0.068
        ARIMA(7, 0, 2) MSE=0.068
        ARIMA(7, 1, 0) MSE=0.068
        ARIMA(7, 1, 1) MSE=0.067
        ARIMA(7, 1, 2) MSE=0.067
        ARIMA(7, 2, 0) MSE=0.094
        ARIMA(8, 0, 0) MSE=0.068
        ARIMA(8, 0, 1) MSE=0.067
        ARIMA(8, 0, 2) MSE=0.067
        ARIMA(8, 1, 0) MSE=0.068
        ARIMA(8, 1, 1) MSE=0.067
        ARIMA(8, 1, 2) MSE=0.067
        ARIMA(8, 2, 0) MSE=0.087
        Best ARIMA(8, 0, 1) MSE=0.067

7. 可视化预测结果与实际结果，计算rmse值(0.36)；
8. 季节、趋势分解有什么用？
9. SARIMAX与ARIMA的区别差异，什么时候用哪个？
10. 参数确定到底是基于平稳还是非平稳序列呢？


ARIMA模型order参数确定：
- https://blog.csdn.net/qq_37135484/article/details/101205161
- https://www.codercto.com/a/41483.html
- PS：ARIMA模型是最复杂的，以上的各个模型都可以认为是特殊参数下的ARIMA；
- d：表示平稳需要的差分阶数，通常为1，通过diff(n)可以平稳处理；
- p(AR)、q(MA)：
    - pq都是由平稳序列的ACF和PACF图中确定；
    - ACF：q阶后衰减趋于零（几何型或震荡性）；
    - PACF：p阶后衰减趋于零（几何型或震荡性）；
    - 即：acf确认q，pacf确认p；
