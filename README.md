# ArgoCD App of Apps
This is an example of how to use the App of Apps pattern with ArgoCD while also making use
of a base helm chart and allowing for overrides.

The `bootstrap` app is the App of Apps and is responsible for deploying the other applications
and needs to be deployed first. You can choose how you want to do this, terraform, pipeline, bash script...who cares.

Once the bootstrap app is deployed, it will start creating all the downstream applications
that will all be visible in a single pane in the argocd UI under the bootstrap app.
However, you will still have individual applications that show up in the UI/CLI as well.

The thought process is that if you just need a change to a single application then 
you just add a value into the valuesl.yaml for that particular application.
If you need global changes that affect all applications, then you can add them to the bootstrap values.

The reason that I don't set `selfHeal` to `true` is because I like to use the argocd-image-updater
and that would get overritten if the self heal option is set. Even when using the git writeback...im sure im doing something
wrong in that workflow cause that makes no sense to me.


