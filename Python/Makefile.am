
CLEANFILES = QuantLib/quantlib_wrap.cpp QuantLib/QuantLib.py .build-stamp

BUILT_SOURCES = QuantLib/quantlib_wrap.cpp QuantLib/QuantLib.py

if HAVE_PYTHON
if BUILD_PYTHON

all-local: .build-stamp

.build-stamp: QuantLib/quantlib_wrap.cpp QuantLib/QuantLib.py setup.py
	CXXFLAGS="$(CXXFLAGS) $(CXXWARNINGFLAGS)" CC="$(CC)" CXX="$(CXX)" $(PYTHON) setup.py build
	touch .build-stamp

check-local: .build-stamp
	$(PYTHON) setup.py test

install-exec-local: .build-stamp
	$(PYTHON) setup.py install

wheel: .build-stamp
	$(PYTHON) setup.py bdist_wheel

clean-local:
	rm -rf build

endif
endif

QuantLib/quantlib_wrap.cpp QuantLib/QuantLib.py: ../SWIG/*.i
	$(SWIG) -python -c++ -outdir QuantLib \
            -o QuantLib/quantlib_wrap.cpp ../SWIG/quantlib.i

dist-hook:
	mkdir -p $(distdir)/examples
	cp ./examples/*.py $(distdir)/examples
	mkdir -p $(distdir)/test
	cp ./test/*.py $(distdir)/test

EXTRA_DIST = README.txt setup.py setup.cfg QuantLib/__init__.py $(BUILT_SOURCES)

