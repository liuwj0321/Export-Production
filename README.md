# Export-Production
Brief introduction
It is determined by NPP multiplied by the export ratio, Here are the three formulas of export ratio used
ef= 0.04756×(0.78-(0.43×SST)/30)×NPP^0.307, (Laws et al., 2011)                        (1)
ef= -0.0081×SST+0.0806×ln⁡(Chla)+0.426, (Dunne et al., 2005)                            (2)
ef= 8.57/(17.9+SST), (Li & Cassar, 2016)                                               (3)



Calculate NPP
%%%lon lat
lats=90:-1/6:-90;
lons=-180:1/6:180;
route='F:\vgpm.2019081.hdf';
hdfinfo(route);
data=hdfread(route,'npp');
npp=data(361:421,1861:1921);%NW
npp1=data(361.5:421.5,1861.5:1921.5);%center
lat=20:1/6:30;%lat
%%% the area of the pixel
a1=cos(deg2rad(lat));
a=cos(deg2rad(lat))*(111.1*111.1/36);
a=a.*1000000;
a=a';
a=flipud(a);
%%% multiply by time
c=day*a.*npp;
c1=day*a.*npp1;
%%%sum over all pixels
d=sum(c(:));
d1=sum(c1(:));



%%%EP
ef1= 0.04756*(0.78-(0.43*SST/30))*npp.^0.307;%NW
ef_1= 0.04756*(0.78-(0.43*SST/30))*npp1.^0.307;%ceanter
%%ef2=-0.0081*SST + 0.0806*log(Chla) + 0.426;
%%ef3=8.57./(17.9 + SST);

EP1=ef1.*npp;
EP_1=ef_1.*npp1;
lat=20:1/6:30;
a1=cos(deg2rad(lat));
a=cos(deg2rad(lat)).*(111.1*111.1./36)*10^6;
a=a';
a=flipud(a);
c=a.*EP1;
c1=a.*EP_1;
d1=sum(c(:));
d_1=sum(c1(:));



