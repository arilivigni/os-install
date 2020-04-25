# os-install
Download release or version that passed ci of OCP which includes the openshift-installer and oc

## Settings and defaults

```
    # OCP cluster install variables
    install_cluster: true
    base_dir: "~/.os-install"
    ocp_install_dir: "{{ base_dir }}/ocp"
    ocp_ci_release: "4.4.0-0.ci"
    ocp_release: "latest"
    ocp_rel_url: "https://mirror.openshift.com/pub/openshift-v4/clients/ocp"
    ocp_ci_api_rel_url: "https://openshift-release.svc.ci.openshift.org/api/v1/releasestream"
    ocp_ci_rel_url: "https://openshift-release-artifacts.svc.ci.openshift.org"
    cluster_name: "ocp-cluster-4"
    cluster_dir:  "{{ base_dir }}/{{ cluster_name }}"
    install_type: "gcp"
    
    # AWS specific
    aws_domain: "devcluster.openshift.com"
    aws_region: "us-east-1"
    
    # GCP specific
    gcp_domain: "gcp.devcluster.openshift.com"
    gcp_project_id: "openshift-gce-devel"
    gcp_region: "us-east4"
    
    # Pull secret and ssh key paths
    pull_secret_file: "~/.gcp/pull-secret.json"
    ssh_key_file: "~/.ssh/id_rsa.pub"
    ssh_key: "{{ lookup('file', ssh_key_file) }}"
    get_release: true
    get_ocp: true
    create_cluster: true
    kubeadmin: "kubeadmin"
    
    # tekton install variables
    install_tekton: true
```

## Examples

### Install cluster in AWS and openshift pipelines (tekton)
```
ansible-playbook -vv -i "localhost," -c local -e cluster_name=my-tekton-cluster install.yml
```

### Install cluster in AWS only
```
ansible-playbook -vv -i "localhost," -c local -e cluster_name=my-tekton-cluster \
    -e install_tekton=false install.yml
```

### Install cluster in AWS with ci version 4.3 of OCP and openshift pipelines (tekton)
```
ansible-playbook -vv -i "localhost," -c local -e cluster_name=my-tekton-cluster \
    -e ocp_ci_release=4.3.0-0.ci \
    -e get_release=false \
    -e install_tekton=false install.yml
```

## Outputs
 
At the end of a run the console url, API url, and the kubeadmin_password are printed.  </br>
They Are also stored in the cluster name directory in the cluster_creds.log.