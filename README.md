����mysql������fetch��bug,ȥ��������fetch�ĵ�һ��table����

	local driver  = require "luasql.mysql"

	--������������
	env = driver.mysql()

	--�������ݿ�
	conn = env:connect("ias_test","root","802802","127.0.0.1",3306)

	--�������ݿ�ı����ʽ
	conn:execute"SET NAMES GB2312"

	--[[
	function rows (connection, sql_statement)
	  local cursor = assert (connection:execute (sql_statement))
	  return function ()
		return cursor:fetch()
	  end
	end

	for id,UserName in rows(conn ,"SELECT id,UserName from user") do
		print(string.format("%s  %s",id,UserName))
	end
	]]--

	--ִ�����ݿ����
	cur = conn:execute("select id,UserName from user")

	print(cur:numrows())

	row = cur:fetch("a")

	while row do
		print(row.id,row.UserName)
		row = cur:fetch("a")
	end

	conn:close()  --�ر����ݿ�����
	env:close()   --�ر����ݿ⻷��