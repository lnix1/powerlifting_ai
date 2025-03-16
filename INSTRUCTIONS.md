# Software Requirements Install Instructions:

This project was developed on a Raspberry Pi 5 with Raspberry Pi OS

## Software for the Camera

The following commands were run in order to download required software for ai camera.

- (These directions were derived from a setup guide: https://www.youtube.com/watch?v=PFfTV4U4QgE&t=180s)

```
sudo apt update && sudo apt full-upgrade
sudo apt install imx500-all
sudo reboot
sudo apt install python3-opencv python3-munkres
```

## Annotation Software

I've opted to go open-source for the annotation software and to not re-invent the wheel here. I'll use Intel's Computer Vision Annotation Software ([cvat.ai](https://www.cvat.ai/)).

I DID NOT run this portion of the project on my raspberry pi. CVAT requires more resources that my poor Pi 5 can bring to bear. Instead, I used a personal machine running Ubuntu 20.04 with an AMD processor and Nvidia 2060 GPU.

Installation and setup instructions [are found here](https://docs.cvat.ai/docs/administration/basics/installation/).

Courses on using the tool can be [found here](https://www.youtube.com/playlist?list=PL0to7Ng4Puua37NJVMIShl_pzqJTigFzg)

# Harware Used:

- [Raspberry Pi AI Camera](https://www.seeedstudio.com/Raspberry-Pi-AI-Camera-p-5939.html?qid=eyJjX3NlYXJjaF9xdWVyeSI6IioiLCJjX3NlYXJjaF9yZXN1bHRfcG9zIjoxLCJjX3RvdGFsX3Jlc3VsdHMiOjE0LCJjX3NlYXJjaF9yZXN1bHRfdHlwZSI6IlByb2R1Y3QiLCJjX3NlYXJjaF9maWx0ZXJzIjoic3RvcmVDb2RlOltyZXRhaWxlcl0gJiYgY2F0ZWdvcnlfaWRzOlsyMjcwXSAmJiBxdWFudGl0eV9hbmRfc3RvY2tfc3RhdHVzOlsxXSJ9)
- [Raspberry Pi Case](https://www.amazon.com/dp/B0CMZG2R73?ref=ppx_yo2ov_dt_b_fed_asin_title)
- [Camera Case](https://www.amazon.com/dp/B0CTN1HCFY?ref=ppx_yo2ov_dt_b_fed_asin_title)
- [Raspberry Pi 5 8GB](https://www.seeedstudio.com/Raspberry-Pi-5-8GB-p-5810.html?qid=eyJjX3NlYXJjaF9xdWVyeSI6IioiLCJjX3NlYXJjaF9yZXN1bHRfcG9zIjozLCJjX3RvdGFsX3Jlc3VsdHMiOjcsImNfc2VhcmNoX3Jlc3VsdF90eXBlIjoiUHJvZHVjdCIsImNfc2VhcmNoX2ZpbHRlcnMiOiJzdG9yZUNvZGU6W3JldGFpbGVyXSAmJiBjYXRlZ29yeV9pZHM6WzIyNTBdICYmIHF1YW50aXR5X2FuZF9zdG9ja19zdGF0dXM6WzFdIn0%3D)
- [Raspberry Pi dual HAT](https://www.seeedstudio.com/PCIe-to-dual-M-2-hat-for-Raspberry-Pi-5-p-5973.html?qid=eyJjX3NlYXJjaF9xdWVyeSI6IioiLCJjX3NlYXJjaF9yZXN1bHRfcG9zIjoyLCJjX3RvdGFsX3Jlc3VsdHMiOjIzLCJjX3NlYXJjaF9yZXN1bHRfdHlwZSI6IlByb2R1Y3QiLCJjX3NlYXJjaF9maWx0ZXJzIjoic3RvcmVDb2RlOltyZXRhaWxlcl0gJiYgY2F0ZWdvcnlfaWRzOlsyMjY3XSAmJiBxdWFudGl0eV9hbmRfc3RvY2tfc3RhdHVzOlsxXSJ9)
- [256GB NVMe M.2 gen 3](https://www.amazon.com/dp/B07ZGK3K4V?ref=ppx_yo2ov_dt_b_fed_asin_title&th=1)
	- Pi 5 cannot make use of the faster speeds of new M.2, so we can save a buck here with an older spec
