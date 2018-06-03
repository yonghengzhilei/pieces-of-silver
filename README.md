jingtum-sdk
------- 
JingtongRequstConstants. URL_HEAD， 可以配置生产环境或测试环境

调用的话，创建对应JingtongRequest，并且赋值对应的参数
然后调用 JingtongRequestUtils.sendRequest(JingtongRequest)，
返回对应的JingtongResponse。

如：查询余额，创建了查询余额`Balances`Request，并且赋值对应数据，返回的是`Balances`Response

BalancesRequest br = new BalancesRequest();

br.setAddress("j4mk8vSKLVhto6RArmQKKGCMW6kc4x68xa");

BalancesResponse jr = (BalancesResponse) JingtongRequestUtils.sendRequest(br);

System.out.println(jr);

assertEquals(true, jr.isSuccess());

		
jingtum-monitordata
------- 
1.监听钱包数据，根据定义的规则，分发数据到业务系统
2.socket监听数据，做到业务实时出发，定时任务监听数据，做到验证socket监听的数据，和补发socket未监听到的数据。
3.数据提交上链
4.数据提交上链之后，监听地址，确认数据上链成功或失败
5.数据上链确认成功或失败，响应到业务系统
![设计](https://github.com/swtcpro/pieces-of-silver/blob/master/jingtum-monitordata/sql/%E7%9B%91%E5%90%AC%E7%B3%BB%E7%BB%9F.png)


commondata
----
封装了一些公共方法和数据，
如，CommitchainMqData，数据上链的消息格式，
DistributeMqData 分发监听到的消息格式，
CommitChainRespMqData 上链结果反馈的消息格式


business-sponsor-sendback
---
业务逻辑，赞赏业务，和回退业务。
