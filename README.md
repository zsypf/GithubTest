# GithubTest
这是我用来学习测试的

if (context.InputParameters.Contains("Target") && context.InputParameters["Target"] is Entity)
            {
                Entity entity = (Entity)context.InputParameters["Target"];
                entity["aiatips_name"] = $"CreatePlugin_" + QueryCount(service);
                entity["aiatips_option"] = new OptionSetValue(594310000);
                entity["aiatips_accountid"] = new EntityReference("account", new Guid("097FF782-624B-EC11-8F8E-002248166E78"));
            }

private int QueryCount(IOrganizationService service)
        {
            QueryExpression query = new QueryExpression("aiatips_students");
            query.ColumnSet.AddColumns("aiatips_name");
            query.Criteria.AddCondition("statecode", ConditionOperator.Equal, 0);
            EntityCollection ec = service.RetrieveMultiple(query);
            return ec.Entities.Count + 1;
        }

        private int QueryCountByFetchXml(IOrganizationService service)
        {
            string fetchXml = @"<fetch version='1.0' output-format='xml-platform' mapping='logical' distinct='false'>
  <entity name='aiatips_students'>
    <attribute name='aiatips_studentsid' />
    <attribute name='aiatips_name' />
    <order attribute='aiatips_name' descending='false' />
    <filter type='and'>
      <condition attribute='statecode' operator='eq' value='0' />
    </filter>
  </entity>
</fetch>";
            EntityCollection ec = service.RetrieveMultiple(new FetchExpression(fetchXml));
            return ec.Entities.Count + 1;
        }
    }
}

