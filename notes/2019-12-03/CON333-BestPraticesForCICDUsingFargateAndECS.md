# CON333 - Best practices for CI/CD using AWS Fargate and Amazon ECS

* ECS:
	- Integrations for:
		- Codepipline
			1. Source
			2. Build
				- Codebuild: "Builds as a service"
					- Good for containers
					- Push images to Amazon ECR
					- buildspec file
					- Container image tagging
						- "latest" is typical tag
					- Source -> Build -> Test -> Production
						- ECS deploys image to test environment
				- Amazon ECR:
					- Immutable image tags
						- Rejects pushes trying to overwrite image tags
						- Protects against updating tags running in production
					- Image scanning
						- Scans for security vulnerabilities
			3. Deployment:
				- GitHub Actions workflow
				- Jenkins
				- Spinnaker pipeline

* Best Practices for CI/CD:
	1. Automated Releases
	2. Safe Reployments
		- Roll back automatically on alarms + validation tests
		- Roll back quickly
		- "Bake" after deployment
		- Deloy small at first, then broadly
		- CodeDeploy:
			- Among other features, rollback automatically if failure is detected
			- Blue/Green deployments
				* App load balancer
				* Production traffic listener
				* Blug target group
				* Blue tasks v1 code
				![](../../images/2019-12-03/CON333-BestPraticesForCICDUsingFargateAndECS_1.png)
				![](../../images/2019-12-03/CON333-BestPraticesForCICDUsingFargateAndECS_2.png)
			- Some problems aren't found until production - a good example of this is compatibility issues with other systems that are current running in production (maybe related to versioning of desparate system)
			- Lifecycle hook:
				- Lambda functions to execute after codedeploy status changes (like a health status code -> deploy service)
			- Deployment group configuration
				- Alarms - automatic rollbacks
				- "Baketime" - how long blue tasks stay around for CodeDeploy terminates it (for fast rollbacks)
			- Safety checks in your deployment pipelines (running `aws cdl` commands in the deployment pipeline)
		- CloudFormation
			- Handy for specifying healthcheck of images in a single, central place
	3. Repeatable Infrastructure Changes:
		- AWS Cloud Development Kit (AWS CCK)
			- Define cloud infrastructure in familiar programming languages (TypeScript, Python, etc...)
			- Many repeated Cloudformation patterns across AWS were being duplicated
				- Tools were introduced for a centralized CloudFormation config storage
				- Pretty cool, these CloudFormation patterns are exposed out as packages, like an npm package.
				![](../../images/2019-12-03/CON333-BestPraticesForCICDUsingFargateAndECS_3.png)
