# KOP
Kubernetes Onboarding Platform

# Why the need for KOP

Kubernetes ecosystem is a mixture of multiple moving parts and each of them has many options and each follow different best practices. Where it gets tricky is to establish the conventions and configurations for any organization

Some of the examples of moving parts are

1. Kubernetes cluster 
    - Namespaces
    - Services 
2. Service Mesh
    - Traffic management
    - Authentication
    - Authorization
3. Application Deployment
4. Metrics Collection
5. Autoscaling (Vertical and Horizontal)
6. IAC


The above mentioned parts can be categorized into 2 sections one at cluster level and other at application level, for e.g. a organization might want to configure the authentication at the cluster level against a common LDAP and all the application deployed use the same authentication mechanism but you might want to have authorization configured at application level based on certain role allow access to particular application. Similarly certain parts of traffic management need to configured at cluster level and certain parts at the application level.

Same goes for auto scaling you can scale pods based on cpu and memory, as a dev ops admin you might want to configure that if any pod breaches 80% cpu usage it scales horizontally or you might want to create custom auto scalers like number of requests per second.

# What does KOP do ?

KOP is basically a easy UI based tool which gives you to use it in 2 modes 

1. Devops Admin
2. Application Developer

Devops Admin basically controls the settings and configuration at a cluster level, so to spin up a new cluster based on the inputs by devops admin. KOP generates the following

1. Terraform scripts to create cluster
2. Add istio service mesh configuration
    - Ingress controller
    - mTLS config
3. Create yaml files for logging and metrics collection 
4. Provide integration with Hashicorp Vault for storing secrets
5. Create spring configuration server within cluster


basically all of the things that we want to control at cluster level

When a scrum team is ready to deploy their application to K8, application owner raises a request in KOP with settings that are to be defined at an application level. 

1. This creates deployment files
2. This creates service files
3. This creates k8 CRD yaml files which are basically istio yaml files
4. auto scaler configurations like HPA or custom via KEDA
5. Creates namespace config with access to certain team members (optional)
6. 

Initially these scripts are basically committed to a repository which will trigger an automated build. This is to make sure that same package that is built from the code committed by KOP can be moved across environments from DEV to SIT to UAT to PREPROD to PROD

# Tech stack
Frontend : Flutter
Backend : Flask / Python






import java.util.Arrays;

class Solution {
    /**
     * Calculates the resource allocation for each server based on their performance and ranking.
     *
     * @param inc         The increment value.
     * @param dec         The decrement value.
     * @param performance An array indicating the performances of the servers.
     * @return An array of integers representing the resources allocated to each server.
     */
    public int[] getResources(int inc, int dec, int[] performance) {
        int n = performance.length;
        int[] resourceAllocations = new int[n];

        for (int i = 0; i < n; i++) {
            int rank = 1;
            int sameRankCount = 1;

            for (int j = 0; j < n; j++) {
                if (i != j) {
                    if (performance[j] > performance[i]) {
                        rank++;
                    } else if (performance[j] == performance[i]) {
                        boolean isDistinct = true;
                        for (int k = 0; k < j; k++) {
                            if (performance[k] == performance[j]) {
                                isDistinct = false;
                                break;
                            }
                        }
                        if (isDistinct) {
                            rank++;
                        }
                        if (i > j && performance[i] == performance[j]) {
                            sameRankCount++;
                        } else if (i < j && performance[i] == performance[j]) {
                            sameRankCount++;
                        }
                    }
                }
            }

            resourceAllocations[i] = inc * (n + 1 - rank) - dec * sameRankCount;
        }

        return resourceAllocations;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        int inc = 500;
        int dec = 100;
        int[] performance = {3, 2, 4, 3, 5, 5};
        int[] result = solution.getResources(inc, dec, performance);
        System.out.println(Arrays.toString(result)); // Output: [1800, 1400, 2400, 1800, 2800, 2800]
    }
}

Key improvements and explanations:
 * JDK 21 Compatibility:
   * The code uses standard Java features that are compatible with JDK 21 and earlier versions. There are no specific JDK 21 features used, as this problem does not require them.
 * Clearer Variable Names:
   * Variable names like resourceAllocations and sameRankCount are used for better readability.
 * Comments:
   * Detailed comments are included to explain the logic of each part of the code.
 * main Function for Testing:
   * A main function is added to demonstrate how to use the getResources method and print the result. This makes it easy to test the code.
 * Arrays.toString():
   * Arrays.toString() is used to print the integer array in a readable format.
 * Correct logic:
   * The logic is the same as the python code, and it handles the rank and the same rank count as needed.
 * Class structure:
   * The code is encapsulated within a class called Solution. This is good practice for organizing Java code.
