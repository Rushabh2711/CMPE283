# Assigment 1
## 1. I have completed this assignment by myself.
## 2. Detail steps I used to complete the assignment.

### Functionality Implemented
- Determines if the CPU supports VMX true controls
- Based on the above, read various MSRs to ascertain support capabilities/features - Entry / Exit / Procbased / Secondary Procbased/ Tertiary Procbased controls / Pinbased controls
- For each group of controls above, interpret and output the values read from the MSR to the system via printk(..), including if the value can be set or cleared.

I am using GDF to discover VMX features present in processor by writing a Linux kernel module that queries these features.

1. Create a project in GDF.

![1](https://user-images.githubusercontent.com/28814244/200367899-04f35486-8827-433d-962c-401a393fe086.PNG)

2. Assign Billing account, Organization and Location to the project.

![2](https://user-images.githubusercontent.com/28814244/200370471-88b93007-1cac-468d-868f-b7efc2143443.PNG)

3. Cretae new VM instance from scratch.

![6](https://user-images.githubusercontent.com/28814244/200370877-e083b70b-a18c-409b-8ca8-7a9f4cbed37a.PNG)

4. Specify Details like, Region, Zone, Disk size, service account, min-cpu-platform etc.

![8](https://user-images.githubusercontent.com/28814244/200370920-06c081ab-de7a-4d4c-8ca2-2de53d851c1f.PNG)
![9](https://user-images.githubusercontent.com/28814244/200371414-433913c8-5f17-4c06-b763-e212ec490a18.PNG)

5. Make sure to enable nested virtualization. here, we are using equivalent command line and run the shell script in google cloud terminal.

> gcloud compute instances create instance-1 --project=cmpe283a1-367906 --zone=us-central1-a --machine-type=n2-standard-8 --network-interface=network-tier=PREMIUM,subnet=default --maintenance-policy=TERMINATE --provisioning-model=STANDARD --service-account=460692059571-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/cloud-platform --min-cpu-platform=Intel\ Cascade\ Lake --create-disk=auto-delete=yes,boot=yes,device-name=instance-1,image=projects/debian-cloud/global/images/debian-11-bullseye-v20221102,mode=rw,size=10,type=projects/cmpe283a1-367906/zones/us-central1-a/diskTypes/pd-balanced --create-disk=auto-delete=yes,device-name=disk-1,image=projects/ubuntu-os-cloud/global/images/ubuntu-2204-jammy-v20221101a,mode=rw,name=disk-1,size=100,type=projects/cmpe283a1-367906/zones/us-central1-a/diskTypes/pd-ssd --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any --enable-nested-virtualization

![11](https://user-images.githubusercontent.com/28814244/200371474-ba0f59bc-9814-48cd-8400-3f02e6b9a969.PNG)

6. created a directory and generate Makefile and cmpe283-1.c file.

![15](https://user-images.githubusercontent.com/28814244/200372284-323215e2-5a7e-4f5d-8940-15542de69b9f.PNG)

7. Install gcc make. Using apt install gcc make command.

> sudo bash <br/>
> apt install gcc make <br/>
> exit <br/>

![16](https://user-images.githubusercontent.com/28814244/200372304-e2d9f2a7-9126-4046-a580-928b16dd9358.PNG)

8. Install Linux Kernal Headers Package

> uname -r <br/>
> sudo apt-get install linux-headers-5.10.0-19-cloud-amd64 <br/>

![17](https://user-images.githubusercontent.com/28814244/200372318-db102701-908c-4a19-9baf-032d31e28c93.PNG)

9. run make command.

> make <br/>
> ls -la

![18](https://user-images.githubusercontent.com/28814244/200372334-ee0efca3-1337-419f-bdaa-0b84959f6141.PNG)

10.Load (insert) the new module. and run the file using dmesg command.

> sudo /sbin/insmod (or rmmod to remove) cmpe283-1.ko <br/>
> sudo dmesg

![19](https://user-images.githubusercontent.com/28814244/200372351-bb5eb6e4-3f12-4c29-825d-8b2d7558aa7c.PNG)

11. Output

I refered this sdm to get more details on MSRs. [Intel sdm vol 3](https://www.intel.com/content/dam/develop/public/us/en/documents/325384-sdm-vol-3abcd.pdf)

IA32_VMX_PINBASED_CTLS 0x481 - Pinbased controls

![20](https://user-images.githubusercontent.com/28814244/200372365-faa0ba55-c02f-420a-ad22-1e0bdaa06f74.PNG)

IA32_VMX_PROCBASED_CTLS 0x482 - Procbased controls

![21](https://user-images.githubusercontent.com/28814244/200372374-9b2978a8-80bd-4a0e-b0d9-2ca45a3c5222.PNG)

A32_VMX_PROCBASED_CTLS2 0x48B - Secondary Procbased controls

![22](https://user-images.githubusercontent.com/28814244/200372388-e9c41f68-9501-4e0f-9fb1-f27fb7210e6f.PNG)

IA32_VMX_EXIT_CTLS 0x483 - Exit controls

![23](https://user-images.githubusercontent.com/28814244/200372409-03f94220-0a74-40a8-8135-dfa96b0e8e9b.PNG)

IA32_VMX_ENTRY_CTLS 0x484 - Entry controls

![24](https://user-images.githubusercontent.com/28814244/200372429-0d8f9538-6cc5-4942-90e5-078e62fb360f.PNG)

IA32_VMX_PROCBASED_CTLS3 0x492 - Tertiary Procbased controls

![25](https://user-images.githubusercontent.com/28814244/200372453-842f14ee-ee90-4aa5-af56-edd70c50631f.PNG)

