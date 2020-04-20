![version](https://img.shields.io/badge/version-1.4-blue)
![pythonversion](https://img.shields.io/badge/Python-3.7-blue)
![idlversion](https://img.shields.io/badge/IDL-8.3-blue)

# OMEGA-Py : Python tools for OMEGA data

Importation and display of OMEGA/MEx observations in Python 3, based on IDL routines developped in the IAS planetary team.

## Installation
Clone the repository and install with pip:

~~~bash
git clone https://git.ias.u-psud.fr/astcherb1/omegapy
cd omegapy
pip3 install .
~~~

## Update
Go to the previously cloned repository, pull the last updates, and install with pip:
~~~bash
cd omegapy
git pull
pip3 install .
~~~

## Configuration
You have to configure the default path of the folders containing the OMEGA binary and omegapy-made files
using the environment variables `OMEGA_BIN_PATH` (for the binary .QUB and .NAV files)
and `OMEGA_PY_PATH` (for the omegapy-made files).

To do so, add the following lines to your `~/.bashrc` :
~~~bash
export OMEGA_BIN_PATH="/data2/opt/geomeg/data/product/"
export OMEGA_PY_PATH="/data/mex-omegj/data1/omega_python/omegapy/"
~~~
*Adapt the path if needed, here is the default configuration for internal IAS use on the server.*

## Usage
~~~python
# package importation
import omegapy.omega_data as od
import omegapy.omega_plots as op
import omegapy.useful_functions as uf
# OMEGA file importation (ORB0964_2)
omega = od.OMEGAdata('0964_2')
# Thermal correction
omega_corr_therm = od.corr_therm(omega)
# Atmospheric correction
omega_corr_therm_atm = od.corr_atm(omega_corr_therm)
# Interactive display of the observation (@ λ = 1.085 µm)
op.show_omega_interactif_v2(omega_corr_therm_atm, lam=1.085, cmap='Greys_r', vmin=0, vmax=0.5, polar=True)
# Search for the index of λ = 1.085 µm in the wavelength array
i_lam = uf.where_closer(1.085, omega.lam)
~~~

See [`docs/*.md`](docs/) or the interactive IPython help for more details.

## Credits
Developped at the Institut d'Astrophysique Spatiale (IAS), Université Paris-Saclay, Orsay, France  

© Aurélien Stcherbinine (2020)
