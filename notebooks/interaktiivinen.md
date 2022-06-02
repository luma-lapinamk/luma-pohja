---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# Interaktiivinen materiaali

Sivulle voidaan tuottaa lukijalle useankaltaista interaktiivista materiaalia sekä myös mahdollistaa sellaisen tuottaminen lukijan toimesta.

## Esimerkki: interaktiivinen kuvaaja

Käytetään **{index}`Thebe`ä** joka mahdollistaa koodisolujen ajamisen suoraan sivulla. Klikkaa raketti-ikonia ja valitse ‘Live Code’. Paina tämän jälkeen ‘run’. 
Säädä liukusäätimillä suoran kulmakerrointa ja vakiotermejä, suoran kuvaaja sekä sen yläpuolella oleva suoran yhtälö päivittyvät automaattisesti.
Kuvaajan tuoton koodit näet klikkaamalla 'Click to show'-painiketta; koodia voi myös muokata haluamakseen ja sitten ajaa (painamalla 'run'); Thebe-tekee
koodisoluista sisällöltään muokattavia ja ajettavia!

```{code-cell} ipython3
:tags: [hide-input, thebe-init]
import numpy as np
import matplotlib.pyplot as plt
import ipywidgets as widgets


def tee_suoran_yhtälön_printtauksen_teksti(kulmakerroin, vakiotermi):
    if np.sign(kulmakerroin) > 0:
        kulmakertoimen_teksti = ''
    else:
        kulmakertoimen_teksti = '-'
    if np.abs(kulmakerroin) != 1:
        kulmakertoimen_teksti += str(np.abs(kulmakerroin))
    vakiotermin_teksti = ''
    if vakiotermi != 0:
        if np.sign(vakiotermi) > 0:
            vakiotermin_teksti += '+'
        else:
            vakiotermin_teksti += '-'
        vakiotermin_teksti += str(np.abs(vakiotermi))
    return 'y = {}x{}'.format(kulmakertoimen_teksti, vakiotermin_teksti)


def suoran_maaritys_ja_plottaus(kulmakerroin, vakiotermi):
    x = np.linspace(-5, 5, 100)
    y = kulmakerroin*x+vakiotermi
    fig, ax = plt.subplots()
    ax.plot(x, y, 'r')
    ax.grid()
    ax.set_xlim([-5, 5])
    ax.set_ylim([-5, 5])
    ax.set_xlabel(r'$x$')
    ax.set_ylabel(r'$y$')
    fig.suptitle(tee_suoran_yhtälön_printtauksen_teksti(kulmakerroin, vakiotermi))
    
    return kulmakerroin, vakiotermi


def suoran_maaritys_ja_plottaus_interaktiivisesti():
    interactive_plot = widgets.interactive(suoran_maaritys_ja_plottaus,
                                           kulmakerroin=widgets.FloatSlider(value=0.1, min=-5, max=5, step=0.1,
                                                                              description='kulmakerroin'),
                                           vakiotermi=widgets.FloatSlider(value=0.0, min=-5, max=5, step=0.1,
                                                                              description='vakiotermi'))
                                          
    return interactive_plot
```

```{code-cell} ipython3
interactive_plot=suoran_maaritys_ja_plottaus_interaktiivisesti()
interactive_plot
```
