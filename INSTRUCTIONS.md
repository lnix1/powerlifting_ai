# Software Requirements Install Instructions:

This project was developed on a Raspberry Pi 5 with Raspberry Pi OS
The following commands were run in order to download required software for ai camera + download example code respository.

- (These directions were derived from a setup guide: https://www.youtube.com/watch?v=PFfTV4U4QgE&t=180s)

```
sudo apt update && sudo apt full-upgrade
sudo apt install imx500-all
sudo reboot
sudo apt install python3-opencv python3-munkres
```

# Harware Used:

- [Raspberry Pi AI Camera](https://www.seeedstudio.com/Raspberry-Pi-AI-Camera-p-5939.html?qid=eyJjX3NlYXJjaF9xdWVyeSI6IioiLCJjX3NlYXJjaF9yZXN1bHRfcG9zIjoxLCJjX3RvdGFsX3Jlc3VsdHMiOjE0LCJjX3NlYXJjaF9yZXN1bHRfdHlwZSI6IlByb2R1Y3QiLCJjX3NlYXJjaF9maWx0ZXJzIjoic3RvcmVDb2RlOltyZXRhaWxlcl0gJiYgY2F0ZWdvcnlfaWRzOlsyMjcwXSAmJiBxdWFudGl0eV9hbmRfc3RvY2tfc3RhdHVzOlsxXSJ9)
- [Raspberry Pi Case](https://www.amazon.com/dp/B0CMZG2R73?ref=ppx_yo2ov_dt_b_fed_asin_title)
- [Camera Case](https://www.amazon.com/dp/B0CTN1HCFY?ref=ppx_yo2ov_dt_b_fed_asin_title)
- [Raspberry Pi 5 8GB](https://www.seeedstudio.com/Raspberry-Pi-5-8GB-p-5810.html?qid=eyJjX3NlYXJjaF9xdWVyeSI6IioiLCJjX3NlYXJjaF9yZXN1bHRfcG9zIjozLCJjX3RvdGFsX3Jlc3VsdHMiOjcsImNfc2VhcmNoX3Jlc3VsdF90eXBlIjoiUHJvZHVjdCIsImNfc2VhcmNoX2ZpbHRlcnMiOiJzdG9yZUNvZGU6W3JldGFpbGVyXSAmJiBjYXRlZ29yeV9pZHM6WzIyNTBdICYmIHF1YW50aXR5X2FuZF9zdG9ja19zdGF0dXM6WzFdIn0%3D)
- [Raspberry Pi dual HAT](https://www.seeedstudio.com/PCIe-to-dual-M-2-hat-for-Raspberry-Pi-5-p-5973.html?qid=eyJjX3NlYXJjaF9xdWVyeSI6IioiLCJjX3NlYXJjaF9yZXN1bHRfcG9zIjoyLCJjX3RvdGFsX3Jlc3VsdHMiOjIzLCJjX3NlYXJjaF9yZXN1bHRfdHlwZSI6IlByb2R1Y3QiLCJjX3NlYXJjaF9maWx0ZXJzIjoic3RvcmVDb2RlOltyZXRhaWxlcl0gJiYgY2F0ZWdvcnlfaWRzOlsyMjY3XSAmJiBxdWFudGl0eV9hbmRfc3RvY2tfc3RhdHVzOlsxXSJ9)
- [256GB NVMe M.2 gen 3](https://www.amazon.com/dp/B07ZGK3K4V?ref=ppx_yo2ov_dt_b_fed_asin_title&th=1)
	- Pi 5 cannot make use of the faster speeds of new M.2, so we can save a buck here with an older spec
