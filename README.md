# GithubTest
这是我用来学习测试的
using Microsoft.Xrm.Sdk;
using Microsoft.Xrm.Sdk.Workflow;

using System.Activities;



namespace Aiden1.Workflow
{
    public class PreCreateStudent : CodeActivity
    {
        [Input("cr73b_name")]
        public InArgument<string> cr73b_name { get; set; }

        [Output("cr73b_lanid")]
        public OutArgument<string> cr73b_lanid { get; set; }
        [Output("cr73b_staffemail")]
        public OutArgument<string> cr73b_staffemail { get; set; }
        [Output("cr73b_groupby")]
        public OutArgument<string> cr73b_groupby { get; set; }

        protected override void Execute(CodeActivityContext executionContext)
        {
            ITracingService tracingService = executionContext.GetExtension<ITracingService>();
            IWorkflowContext context = executionContext.GetExtension<IWorkflowContext>();
            IOrganizationServiceFactory serviceFactory = executionContext.GetExtension<IOrganizationServiceFactory>();
            IOrganizationService service = serviceFactory.CreateOrganizationService(context.UserId);

            var key = cr73b_name.Get(executionContext);
            tracingService.Trace(key);
            cr73b_lanid.Set(executionContext, $"AidenVS:" + key);
            cr73b_staffemail.Set(executionContext, $"AidenVS1:" + key);
            cr73b_groupby.Set(executionContext, $"AidenVS1:" + key);
        }
    }
}

