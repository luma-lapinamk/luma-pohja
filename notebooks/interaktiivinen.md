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

## Esimerkki: interaktiiviset koodisolut ja interaktiivinen kuvaaja

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

Alla koodisolu, jota voidaan myös ajaa ja muokata.  

```{code-cell} ipython3
# oppimateriaaliin mahd. hyvä laittaa tämänlaisia soluja
# lukijalle, joita lukija voi muokata ja käyttää
# "koodailuun"  
```

Täppiä erilaisiin juttuihin, esim. eri vaikeustaso, ja/tai vaikka sisältötyyppi.  
Seuraavaksi esimerkki:

`````{tab-set}

````{tab-item} Helppo
Kokeile keskiarvo- ja keskihajonta-parametrien sekä näytteiden lukumäärän 
vaikutusta sirontakaavioon. Käytä ylläolevaa ajettavaa koodisolua koodailuun 
ja koodin ajamiseen.

```ipython3
# Muokkaa -----------------> 
x_1_mean = 0.
x_2_mean = 0.
standard_deviation = 1.
num_datapoints = 100  
# <----------------- Muokkaa
mean = np.array([[x1_mean, x2_mean]])
data = mean+standard_deviation*np.random.randn((num_datapoints, 2))
plt.scatter(data[:, 0], data[:, 1], 'r')
```
````

````{tab-item} Vaikeampi
Poimitaan näytteitä kaksiulotteisesta normaalijakaumasta. 
Alla oleva koodi on virheellinen yhdellä rivillä. Korjaa virhe sekä
kokeile keskiarvo- ja keskihajonta-parametrien sekä näytteiden lukumäärän 
vaikutusta sirontakaavioon. Käytä ylläolevaa ajettavaa koodisolua koodailuun 
ja koodin ajamiseen.  

```ipython3
# Muokkaa -----------------> 
x_1_mean = 0.
x_2_mean = 0.
standard_deviation = 1.
num_datapoints = 100  
# <----------------- Muokkaa
mean = np.array([[x1_mean, x2_mean]])
# Muokkaa -----------------> 
data = np.random.randn((num_datapoints, 2)) # virheellinen
# <----------------- Muokkaa
plt.scatter(data[:, 0], data[:, 1], 'r')
```
````

````{tab-item} Vaikein
Tee koodi jossa poimitaan näytteitä kaksiulotteisesta normaalijakaumasta,
sekä tehdään näytteistä sirontakaavio. Oleta, että satunnaismuuttujien välillä
on korrelaatiota. Tee koodi sellaiseksi, että korrelaatiokerrointa voidaan 
helposti säätää ja tutkia. Käytä ylläolevaa ajettavaa koodisolua koodailuun 
ja koodin ajamiseen.

```ipython3
# lisää koodisi tänne
```
````

````{tab-item} Tehtävän tarkoitus
Tehtävän tarkoitus on demonstroida miten poimitaan näytteitä moniulotteisesta
normaalijakaumasta ja näytteiden visualisointia sirontakaaviolla. 
````
`````
