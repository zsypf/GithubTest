# GithubTest
这是我用来学习测试的

using Microsoft.Xrm.Sdk;
using Microsoft.Xrm.Sdk.Query;
using Microsoft.Xrm.Sdk.Workflow;

using System.Activities;



namespace Aiden1.Workflow
{
    public class PreCreateStudent : CodeActivity
    {
        [Input("cr73b_staffemail")]
        public InArgument<string> cr73b_staffemail { get; set; }

        [Output("cr73b_lanid")]
        public OutArgument<string> cr73b_lanid { get; set; }

        [Output("cr73b_groupby")]
        public OutArgument<string> cr73b_groupby { get; set; }

        protected override void Execute(CodeActivityContext executionContext)
        {
            ITracingService tracingService = executionContext.GetExtension<ITracingService>();
            IWorkflowContext context = executionContext.GetExtension<IWorkflowContext>();
            IOrganizationServiceFactory serviceFactory = executionContext.GetExtension<IOrganizationServiceFactory>();
            IOrganizationService service = serviceFactory.CreateOrganizationService(context.UserId);
            var key = cr73b_staffemail.Get(executionContext);
            tracingService.Trace(key);
            QueryCount(service,key, tracingService);
            cr73b_lanid.Set(executionContext, QueryCount(service, key, tracingService));
            cr73b_groupby.Set(executionContext, QueryCount(service, key, tracingService));

        }
        private string QueryCount(IOrganizationService service,string abc, ITracingService tracingService)
        {
            
            QueryExpression query = new QueryExpression("cr73b_staff_campagin");
            query.ColumnSet.AddColumns("cr73b_lanid", "cr73b_groupby");
            query.Criteria.AddCondition("cr73b_staffemail", ConditionOperator.Equal, abc);
            EntityCollection ec = service.RetrieveMultiple(query);
            ec.Entities[0].GetAttributeValue<string>("cr73b_lanid");
            if (ec.Entities.Count > 0)
            {
                tracingService.Trace("123");
                if (ec.Entities[0].Contains("cr73b_lanid"))
                {
                    string test;
                    tracingService.Trace("aaaaaaaaaaaaaaaa");
                    test = ec.Entities[0].GetAttributeValue<string>("cr73b_lanid");
                    tracingService.Trace("bbbbbbbbbbbbbbbb"+test);
                    return test;
                }
                else
                {
                    return "false-aiden";
                }
                
            }
            else
            {
                tracingService.Trace("456");
                return "aiden:1111111111";
            }
        }
    }
}


