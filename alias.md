The following aliases helped me in saving time by reducing the keystrokes.

Alias to create the kubernetes object using the manifest or configuration file:
<code>
<br>alias kc='kubectl create -f'
</code>

Alias to update the existing kubernetes object using the manifest or configuration file:
<code>
<br>alias kr='kubectl replace --force --grace-period 0 -f'
</code>

Alias to view the existing kubernetes object using the manifest or configuration file:
<code>
<br>alias kg='kubectl get -f'
</code>

Alias to set the namespace:
<code>
<br>alias kn='kubectl config set-context --current --namespace='
</code>

Alias to describe the kubernetes object's status, events and more details:
<code>
<br>alias kd='kubectl describe'
</code>