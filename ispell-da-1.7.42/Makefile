LANG=da_DK.ISO8859-1

sprog=dansk
sprog_en=Danish
sprog_en_lower_case=danish
language_code=da
country_code=DK

lang=da
version=1.7.42

installdir=`ispell -vv | grep LIBDIR | cut -d'"' -f2`

all: maskbits $(sprog).hash

maskbits:
	@test "`ispell -vv | grep MASKBITS`" != ""              || ( echo Ispell should be compiled with MASKBITS set to at least 64. ; exit -2 )
	@test `ispell -vv | grep MASKBITS | cut -d= -f2` -ge 64 || ( echo Ispell should be compiled with MASKBITS set to at least 64. ; exit -3 )

install: maskbits $(sprog).hash $(sprog).aff
	install -o root -g root -m 0644 $(sprog).hash $(installdir)
	install -o root -g root -m 0644 $(sprog).aff $(installdir)
	ln -fs $(installdir)/$(sprog).hash $(installdir)/$(language_code)_$(country_code).hash
	ln -fs $(installdir)/$(sprog).aff  $(installdir)/$(language_code)_$(country_code).aff
	ln -fs $(installdir)/$(sprog).hash $(installdir)/$(sprog_en_lower_case).hash
	ln -fs $(installdir)/$(sprog).aff  $(installdir)/$(sprog_en_lower_case).aff

$(sprog).hash: maskbits $(sprog).aff words-$(language_code).ispell
	buildhash words-$(language_code).ispell $(sprog).aff $(sprog).hash

clean:
	rm -f words-$(language_code).ispell.stat $(sprog).hash words-$(language_code).ispell.cnt *~
