```fortran
!---------------------------------------------------------------------------------------

! This program computes the flux surfaces - Az by reading the the inplane magnetic field

! components from data/bx.gda and data/bz.gda, taking the curl, and solving the needed

! Poisson equation

!

! This version is for a single sheet - periodic in x, with conducting BC in z

!---------------------------------------------------------------------------------------

  
  

module fft

implicit none

integer(kind=8) forward,inverse

real(kind=8) norm,kx,pi

real(kind=8), allocatable, dimension(:) :: kx2,in,out

INTEGER FFTW_PATIENT

PARAMETER (FFTW_PATIENT=32)

INTEGER FFTW_R2HC

PARAMETER (FFTW_R2HC=0)

INTEGER FFTW_HC2R

PARAMETER (FFTW_HC2R=1)

INTEGER FFTW_RODFT00

PARAMETER (FFTW_RODFT00=7)

INTEGER FFTW_RODFT01

PARAMETER (FFTW_RODFT01=8)

INTEGER FFTW_RODFT10

PARAMETER (FFTW_RODFT10=9)

INTEGER FFTW_REDFT01

PARAMETER (FFTW_REDFT01=4)

INTEGER FFTW_REDFT10

PARAMETER (FFTW_REDFT10=5)

end module fft

  
  

program translate

use fft

use hdf5

implicit none

integer input_record,output_record,input_error,output_error,record_length,it1,it2,i,j,it,interval

integer(kind=4) :: nx,ny,nz

real(kind=4) :: diff,xmax,ymax,zmax,time

real(kind=4), allocatable, dimension(:,:) :: bx,by,Az,curlb

real(kind=4), allocatable, dimension(:,:,:) :: tmp_array

real(kind=8) :: dx,dy

logical :: hdf5_fields ! whether fields are saved in HDF5 format

character(len=8) :: cit

character(len=128) :: filename, groupname

integer(hid_t) :: file_id, group_id, dataset_id, filespace

integer(hsize_t), dimension(3) :: dset_dims, dset_dims_max

integer :: error

  

! Range of time slices to convert. Make big and let error terminate program

it1 = 0

it2 = 22

interval = 353

hdf5_fields = .true.

output_record = 0

  

! ! Open data information file to find out the size of the arrays

! open(unit=10,file='data/info',access='stream',status='old',form='unformatted')

! ! Read data from info file

! read(10)nx,ny,nz

! read(10)xmax,ymax,zmax

! close(10)

  

nx = 2048

ny = 2048

nz = 1

xmax = 512.0

ymax = 512.0

zmax = 0.25

  

! Cell size

  

dx = xmax/real(nx)

dy = ymax/real(ny)

  

! Echo this information

  

print *,"---------------------------------------------------"

print *,"xmax=",xmax," ymax=",ymax

print *,"nx=",nx," ny=",ny

print *,"dx=",dx," dy=",dy

print *,"---------------------------------------------------"

  

! Initialize FFT library

  

allocate(in(nx))

allocate(out(nx))

norm = 1.0d0/sqrt(real(nx))

call dfftw_plan_r2r_1d(forward,nx,in,out,FFTW_R2HC,FFTW_PATIENT)

call dfftw_plan_r2r_1d(inverse,nx,in,out,FFTW_HC2R,FFTW_PATIENT)

  

! Wavectors in x direction ( Half-Complex Format )

! See page 10 of FFTW-3.0 manual for description

  

allocate(kx2(nx))

pi = acos(-1.0d0)

kx2(1)=0.0d0

do j=1,nx/2

kx = (2.0d0*pi*real(j)/xmax)

diff = sin(kx*dx/2.0d0)/(kx*dx/2.0d0)

kx2(j+1) = (kx*diff)**2

enddo

do j=1,(nx+1)/2-1

kx = (2.0d0*pi*real(j)/xmax)

diff = sin(kx*dx/2.0d0)/(kx*dx/2.0d0)

kx2(nx+1-j) = (kx*diff)**2

enddo

  

! Allocate storage space for fields and moments

  

allocate(bx(nx,ny))

allocate(by(nx,ny))

allocate(Az(nx,ny))

allocate(curlb(nx,ny))

allocate(tmp_array(ny,nx,1))

  

! Set record length for gda files

  

! Use this for Bill's gda format with extra time and it records

! inquire(iolength=record_length)bx,time,it

  

! Use this if you are only saving the matrix in the gda file

inquire(iolength=record_length)bx

  

! *** WARNING - also make the read statments below consistent ***

  

print *," Setting record length=",record_length

  

! Open all of the direct access binary files (Bill's preferred data format)

! Loop over time slices

  

do input_record = it1,it2

write(cit,'(I0)') input_record * interval

print *,"Reading record=",input_record

  

if (hdf5_fields) then

call h5open_f(error)

filename = "field_hdf5/T."//trim(cit)//"/fields_"//trim(cit)//".h5"

groupname = "Timestep_"//trim(cit)

call h5fopen_f(filename, H5F_ACC_RDWR_F, file_id, error, &

access_prp=h5p_default_f)

call h5gopen_f(file_id, groupname, group_id, error)

  

! bx

call h5dopen_f(group_id, "cbx", dataset_id, error)

call h5dget_space_f(dataset_id, filespace, error)

call h5Sget_simple_extent_dims_f(filespace, dset_dims, dset_dims_max, error)

call h5dread_f(dataset_id, H5T_NATIVE_REAL, tmp_array, dset_dims, error)

call h5sclose_f(filespace, error)

call h5dclose_f(dataset_id, error)

bx = transpose(tmp_array(:,:,1))

  

! by

call h5dopen_f(group_id, "cby", dataset_id, error)

call h5dget_space_f(dataset_id, filespace, error)

call h5Sget_simple_extent_dims_f(filespace, dset_dims, dset_dims_max, error)

call h5dread_f(dataset_id, H5T_NATIVE_REAL, tmp_array, dset_dims, error)

call h5sclose_f(filespace, error)

call h5dclose_f(dataset_id, error)

by = transpose(tmp_array(:,:,1))

  

call h5gclose_f(group_id, error)

call h5fclose_f(file_id, error)

else

open(unit=20,file='data/bx.gda',access='direct',&

recl=record_length,status='unknown',form='unformatted',action='read')

open(unit=30,file='data/by.gda',access='direct',&

recl=record_length,status='unknown',form='unformatted',action='read')

  

! Read magnetic field data

  

read(20, rec=input_record+1)bx

read(30, rec=input_record+1)by

close(20)

close(30)

endif

  

! Compute Curl of magnetic field

  

print *,"Computing curl"

  

do i=2,nx-1

do j=2,ny-1

curlb(i,j) = (by(i+1,j)-by(i-1,j))/(2.0*dx) - (bx(i,j+1)-bx(i,j-1))/(2.0*dy)

! curlb(i,j) = (bx(i,k,j+1)-bx(i,k,j-1))/(2.0*dz) - (bz(i+1,k,j)-bz(i-1,k,j))/(2.0*dx)

enddo

enddo

curlb(1,:) = curlb(2,:) ! not sure about it

curlb(nx,:) = curlb(nx-1,:)

curlb(:,1) = curlb(:,ny-1)

curlb(:,ny) = curlb(:,2)

  

! Solve Poisson equation

  

print *,"Solving Poisson"

call poisson(dx,nx,dy,ny,curlb,Az,bx)

  

! Save flux surfaces

  

print *,"Saving Az"

output_record = output_record +1

open(unit=40,file='data/Az.gda',access='direct', &

recl=record_length,status='unknown',form='unformatted',action='write')

open(unit=41,file='data/Bx.gda',access='direct', &

recl=record_length,status='unknown',form='unformatted',action='write')

open(unit=42,file='data/By.gda',access='direct', &

recl=record_length,status='unknown',form='unformatted',action='write')

!write(40,rec=output_record)Ay,time,it

write(40,rec=output_record)Az

write(41,rec=output_record)bx

write(42,rec=output_record)by

close(40)

close(41)

close(42)

enddo

  

deallocate(in, out)

deallocate(kx2)

deallocate(bx, by, Az, curlb, tmp_array)

end program translate

  

subroutine poisson(dx,nx,dy,ny,rho,phi,bx)

use fft

implicit none

integer nx,ny,i,j

real(kind=4) phi(nx,ny),rho(nx,ny),bx(nx,ny)

real(kind=8) dx,dy,dx2,dy2,ak(nx,ny)

real(kind=8) d(ny),g(ny),w(ny),rhs(ny),cycle(nx,ny)

real(kind=8) error,maxerror,delsq,bsum

  

! Do internal calculation in double precision to avoid round-off on large grids

  

! Constants

  

dy2 = dy**2

dx2 = dx**2

  

! fft in x-direction

do j=1,ny

in(:) = -dy2*real(rho(:,j),kind=8)

call dfftw_execute(forward)

ak(:,j) = norm*out(:)

enddo

  

! Now do a tri-diagonal solve across the y-direction

  

do i=1,nx

d(:) = -2.0d0 - dy2*kx2(i)

d(1) = -3.0d0 - dy2*kx2(i) ! phi=0 at z=0

d(ny) = -3.0d0 - dy2*kx2(i) ! phi = 0 at z=zmax - fix this below

w(1) = 1.0d0/d(1)

g(1) = ak(i,1)/d(1)

do j=2,ny

w(j) = 1.0d0/(d(j)-w(j-1))

g(j) = (ak(i,j)-g(j-1))*w(j)

enddo

ak(i,ny) = g(ny)

do j=ny-1,1,-1

ak(i,j) = g(j) - w(j)*ak(i,j+1)

enddo

enddo

  

! Now take inverse FFT

  

do j=1,ny

in(:) = ak(:,j)

call dfftw_execute(inverse)

ak(:,j) = norm*out(:)

enddo

  

! Now add correction for oblique or asymmetric layers

  

bsum = 0.0d0

do i=1,nx

do j=1,ny

bsum = bsum + bx(i,j)

enddo

enddo

bsum = -bsum/real(ny*nx)

  

do i=1,nx

do j=1,ny

ak(i,j) = ak(i,j) + bsum*real(j-ny/2)*dy

enddo

enddo

  

! Do error check on solution

  

maxerror = 0.0

do i=2,nx-1

do j=2,ny-1

delsq = (ak(i+1,j)-2.0*ak(i,j)+ak(i-1,j))/dx2 + (ak(i,j+1)-2.0*ak(i,j)+ak(i,j-1))/dy2

error = abs(real(rho(i,j),kind=8) + delsq)

if (error > maxerror) maxerror=error

enddo

enddo

print *,"Error in poisson solve = ", maxerror

  

! Return solution in single precision

phi(:,:) = real(ak(:,:),kind=4)

return

end subroutine poisson
```