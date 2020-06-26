# How Debugger Works<a name="debugger-how-it-works"></a>

With Amazon SageMaker Debugger, you can go beyond just looking at scalars, like losses and accuracies, when evaluating model training\. Debugger gives you full visibility into a training job by using a *hook* to capture tensors that define the state of the training process at each point in the job's lifecycle\. Debugger also provides *rules* to inspect the captured tensors\. 

Built\-in *rule*s monitor the training flow and alert you to problems with common conditions that are critical for the success of the training job\. You can also create your own custom rules to watch for any issues specific to your model\. You can monitor the results of the analysis done by rules with Amazon CloudWatch events, using an Amazon SageMaker notebook, or in visualization provided by Amazon SageMaker Studio\.

The following diagram shows the flow for the model training process with Amazon SageMaker Debugger\.

![\[Overview of how Amazon SageMaker Debugger works.\]](http://docs.aws.amazon.com/sagemaker/latest/dg/images/how-debugger-works-4.png)

To use Amazon SageMaker Debugger hooks and rules, you activate them by adding only a few lines of code in your estimator object\. Debugger and its client library `smdebug` help you set up hooks and rules that give you transparency into training jobs\. Debugger and `smdebug` support the major machine learning frameworks—TensorFlow, MXNet, and PyTorch—and the Amazon SageMaker pre\-built algorithm XGBoost, while you run training jobs in the Amazon SageMaker environment\. 
+ **Choose a framework and use Amazon SageMaker pre\-built training containers: ** Amazon SageMaker gives you options to use Amazon pre\-built training containers or custom containers to run training jobs\. Debugger features and pre\-built training containers such as Amazon SageMaker containers and Deep Learning Containers help make your model debugging process budget\-friendly\. You can also bring your own containers if you prefer to customize Debugger for your training algorithms\. To learn more, go to [Use Containers in Frameworks Supported by Debugger](debugger-container.md)\. 
+ **Use a Debugger hook to save tensors: ** After you choose a container and a framework that fit your training script, use a Debugger hook to configure which tensors to save and to which directory to save them, such as a Amazon S3 bucket\. A Debugger hook helps you to build the configuration and to keep it in your account to use in subsequent analyses, where it is secured for use with the most privacy\-sensitive applications\. To learn more, go to [ Save Tensor Data Using the Debugger Hook API](debugger-data.md)\. 
+ **Use Debugger rules to inspect tensors in parallel with a training job: ** To analyze tensors, Debugger provides built\-in rules for over a dozen abnormal training process behaviors\. For example, a Debugger rule detects issues when the training process suffers from vanishing gradients, exploding tensors, overfitting, or overtraining\. If necessary, you can build customized rules to analyze saved tensors using the Amazon SageMaker Debugger SDK\. You can then use the Amazon SageMaker Python SDK to configure Debugger to save the required tensors and to deploy built\-in or custom rules for monitoring them\. To learn more, go to [How to Use Built\-in Rules for Model Analysis](use-debugger-built-in-rules.md), [List of Built\-in Rules Provided by Amazon SageMaker Debugger](debugger-built-in-rules.md) for the full Debugger rule API, and [How to Use Custom Rules](debugger-custom-rules.md) for customizing Debugger rules\. In combination with Debugger rules, you can also use Amazon CloudWatch Events to call an AWS Lambda function that automatically stops the training job when the Debugger rules trigger `"IssuesFound"` status\.
+ **Create *trial*s to analyze tensors: **The `smdebug` trial is an object that lets you query the saved tensors from a given training job, specified by the path to which `smdebug` artifacts are saved\. A trial is capable of loading new tensors as they become available at a given path, enabling you to do both offline and real\-time analysis\. To learn more about the smdebug trial, see [ the smdebug trial API](https://github.com/awslabs/sagemaker-debugger/blob/master/docs/analysis.md#trial-api)\. 
+ **Use Amazon SageMaker studio for visualization: ** You can use Debugger in Amazon SageMaker Studio for visulizing collected trials by Debugger\. Amazon SageMaker Studio makes inspecting training job issues easier through its visual interface for analyzing your tensor data\. To learn more, go to [Amazon SageMaker Studio Visualizations of Model Analysis Results with Debugger](debugger-visualization.md)\. 